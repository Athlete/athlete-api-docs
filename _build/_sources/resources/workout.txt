Workouts
========

Fetch all workouts for a user
-----------------------------

**GET /workout/**

    :user: The id of the user who's workouts you want

Response

::

    [
        {
          "distance_in_meters": "8046.72",
          "duration_in_seconds": 1500,
          "id": 2,
          "post_body": "great",
          "resource_uri": "/api/v1/workout/2/",
          "route_points_data": "",
          "run_date": "2012-05-22T00:00:00",
          "run_type": "Endurance",
          "static_map_url": "http://some.domain/super-long-url",  // <-- this will sometimes be null
          "title": "Running"
        }
    ]


You can also get a workout in GPX format. To accomplish this, you must specify the right "Accept" header:

**GET /workout/**
**Accept: application/X.athlete-GPX+xml**

You'll get some headers and the content in the response body:

::

    200 Ok
    Content-Type: application/X.athlete-GPX+xml; charset=utf-8

    <?xml version='1.0' encoding='utf-8'?>
    <gpx xmlns="http://www.topografix.com/GPX/1/1" version="1.1" creator="Athlete.com">
        <metadata>
            <author>
                <name>Athlete.com</name>
            </author>
            <time>2012-06-27T12:12:39Z</time>
        </metadata>
        <trk>
            <name>Endurance - Running</name>
            <trkseg>
                <trkpt lon="-111.94151446223259" lat="40.855995789170265">
                    <ele>1291.0</ele>
                    <time>2012-03-11T00:33:47.000Z</time>
                </trkpt>
                <trkpt lon="-111.94152887910604" lat="40.85599763318896">
                    <ele>1291.0</ele>
                    <time>2012-03-11T00:33:48.000Z</time>
                </trkpt>
                ...
            <trkseg>
        <trk>
    </gpx>


Create a workout with GPX data
------------------------------

**POST /workout/**

The prefered method to POST (create a new workout) is with a throught a GPX representation. You must specify the Content-Type header as "application/X.athlete-GPX+xml" (See below for details about content types).

Here's an example of a POST request containing a GPX representation (Headers removed for brevity):

::

    <?xml version="1.0" encoding="UTF-8"?>
    <gpx version="1.1" creator="Athlete Mobile App (Not important)"
        xsi:schemaLocation="http://www.topografix.com/GPX/1/1"
        xmlns="http://www.topografix.com/GPX/1/1">
        <metadata>
            <desc>Run description</desc>
            <time>2012-07-02T12:03:38Z</time>
            <extensions>
                <privacy>private</privacy>
		<facebook_access_token>FacebookTokenHere!</facebook_access_token>
            </extensions>
        </metadata>
        <trk>
            <name>Run around the park</name>
            <type>Endurance</type>
            <trkseg>
                <trkpt lon="-113.635201" lat="37.1570545">
                    <time>2012-07-01T17:00:00Z</time>
                    <ele>900.567032295</ele>
                </trkpt>
                ... More Points ...
            <trkseg>
        </trk>
    </gpx>

I'll describe the most important data there:

    :metadata/desc: The post body. The description to the workout (it's going to be saved as Post information).
    :metadata/time: The datetime when the workout was created. The format is like the example. [YEAR]-[MONTH]-[DAY]T[HOUR]:[MINUTE]:[SECONDS]Z.

    :trk/name: The name of the workout. The title the user assigned to it.
    :trk/type: The type of the run as described above. (Endurance, Indoor, Beach, etc.)
    :trk/trkseg: Here you put the points!

    :metadata/extensions/privacy: The privacy of the workout. Allowed values are [public, friends, private]. This field is optional, if you don't provide a privacy value, "public" will be used.[OPTIONAL]
    :metadata/extensions/facebook_access_token: If you provide a valid Token, this workout will be shared on facebook. [OPTIONAL]

Each <trkpt> element contains the route data.

GPX Documentation: http://www.topografix.com/GPX/1/1/

Create a workout with JSON data
------------------------------

**POST /workout/**

You can also upload a workout from a JSON document. You must use the Content-type header "application/json".

Arguments

These arguments contain hierarchical data (see *points*) so you'll need to use an application/xml or application/json
content type.

Note that workouts (and posts) can also have attached images. Those must be posted separately.

    :run_date: A DateTime in format ISO 8601 format
    :title: The run title (whatever the user wants to call this run)
    :post_body: An optional argument containing a text post about this run.
    :run_type: Must be one of Endurance, Tempo, Slow, Interval, Group, Elevation, Race
    :duration_in_seconds: The duration of the run, in seconds. If the user paused during that run, that time should not be included.
    :distance_in_meters: The distance of the run in meters.
    :privacy: The privacy level for this workout. Options: "public", "private", "friends". [OPTIONAL]
    :facebook_access_token: If you provide a valid Token, this workout will be shared on facebook. [OPTIONAL]
    :points: An optional array of objects, each containing the following attributes:
        :lat: The latitude
        :lng: The longitude
        :time: The date/time that this data point was recorded in ISO 8601 format
        :elev: The elevation at this data point (if available). Synonymous with altitude.


Example of a Workout document to POST (https://gist.github.com/3525174)

::

    {
        "run_date": "1970-01-01T00:00:00Z",
        "title": "Run Title!",
        "run_type": "Endurance",
        "duration_in_seconds": 3600,
        "distance_in_meters": 1000,
        "post_body": "This is the body, in order to provide a full description of your run",
        "privacy": "public",
        "points": [
            {
                "lng":"-111.5373066",
                "lat":"40.7231711",
                "time": "2012-01-01T00:00:04Z",
                "elev": "1942.1789265256325"
            },
            {
                "lng":"-111.5372056",
                "lat":"40.7228762",
                "time": "2012-01-01T00:00:07Z",
                "elev": "1942.109892409177"
            }
        ]
    }


Delete a workout
----------------

**DELETE /workout/[workout_id]/**

Response

    Not sure. Nothing of importance.
    You will get a 401 UNAUTHORIZED response if the current logged in user does not own the workout.

Upload route data to a workout
------------------------------

This method allows you to send GPX files containing routes data for some Workout. You must specify the Workout ID. You must own that workout in order to update the route data. Right now the only file suported is GPX, we might add support to other formats in the future. Stay in touch for updates on this topic.

**PATCH /workout/[workout_id]/**

You must send the Content-Type of the file (see below) and the entire file as the request body.

Share a workout
-----------------------------

**POST /workout/[ID]/share/**

    :social_network: The network where you want to publish this workout. Right now, it's just "facebook".
    :token: The access token for the network you want to share this workout to.

The response will be a Json Object, the response code is allways 200. You can check if the sharing was succesful by the body of the response:

{'success': false}

We always return a 'success' key with a true/false value to indicate if the share was sucessful. Also, depending on the network you're sharing, other fields might be included. For example, this is a response for a valid share in Facebook:

{
  "post_id": "605471098_442971085741556",
  "success": true
}

Content Types
--------------

Currently, there are not official content types for the supported files, so we agree in this content types:

* "application/X.athlete-GPX+xml" -> for GPX data

Please remove the quotes and be careful with uppercase letters.
