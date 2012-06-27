Workouts
========

Fetch all workouts for a user
-----------------------------

**GET /workout/**

    :user: The id of the user who's workouts you want

Response

::

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


You can also get a workout in GPX format. To accomplish this, you must specify the right "Accept" header:

**GET /workout/**
**Accept: application/X.athlete-GPX+xml**

You'll get some headers and the content in the response body:

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

Create a workout
----------------

**POST /workout/**

Arguments

These arguments contain hierarchical data (see *points*) so you'll need to use an application/xml or application/json
content type.

Note that workouts (and posts) can also have attached images. Those must be posted separately. **This is not implemented yet**

    :run_date: A DateTime in format ISO 8601 format
    :title: The run title (whatever the user wants to call this run)
    :post_body: An optional argument containing a text post about this run.
    :run_type: Must be one of Endurance, Tempo, Slow, Interval, Group, Elevation, Race
    :duration_in_seconds: The duration of the run, in seconds. If the user paused during that run, that time should not be included.
    :distance_in_meters: The distance of the run in meters.
    :points: An optional array of objects, each containing the following attributes:
        :lat: The latitude
        :lng: The longitude
        :time: The date/time that this data point was recorded in ISO 8601 format
        :elev: The elevation at this data point (if available). Synonymous with altitude.

Example of a Workout document to POST

::

    {
        "run_date": "1970-01-01T00:00:00Z",
        "title": "Run Title!",
        "run_type": "Endurance",
        "duration_in_seconds": 3600,
        "distance_in_meters": 1000,
        "post_body": "This is the body, in order to provide a full description of your run",
        "points": [
            {
                "lng":"-111.5373066",
                "lat":"40.7231711",
                "time": "2012-01-01T00:00:04Z",
                "ele": "1942.1789265256325"
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

Content Types
--------------

Currently, there are not official content types for the supported files, so we agree in this content types:

* "application/X.athlete-GPX+xml" -> for GPX data

Please remove the quotes and be careful with uppercase letters.
