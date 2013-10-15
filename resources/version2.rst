Version 2
=========

The new version of the API (v2) is intended to provide the functionality needed to handle workouts with type and subtype. The previous version of the app (v1) only supported "Running" workouts. We now support all these activity types:

* Running
* Walking
* Cycling
* Hiking
* Mountain Biking
* Wheelchair
* Paddling
* X-Country Skiing
* Downhill Skiing
* Snowboarding
* Swimming

Each activity type supports different activity subtypes.

Workout resource changes
------------------------

Workouts have now 2 new attributes: ``activity_type`` and ``activity_subtype``. This is the JSON representation of an example workout (with points):

::

    {
        "run_date": "1970-01-01T00:00:00Z",
        "title": "Run Title!",
        "activity_subtype": "Running",
        "activity_subtype": "Endurance",
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

You can see the third and fourth arguments are ``activity_type`` and ``activity_subtype``. The remaining of the representation is the same as v1. A basic description of the new fields for reference:

    :activity_type: The activity type of the workout (listed above).
    :activity_subtype: The activity subtype. See activity types section for details.

Both these attributes are mandatory. You have to provide both. We don't accept defaults.

This is a **GPX representation** of the v2:

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
                <subtype>Endurance</subtype>
            </extensions>
        </metadata>
        <trk>
            <name>Run around the park</name>
            <type>Running</type>
            <trkseg>
                <trkpt lon="-113.635201" lat="37.1570545">
                    <time>2012-07-01T17:00:00Z</time>
                    <ele>900.567032295</ele>
                </trkpt>
                ... More Points ...
            <trkseg>
        </trk>
    </gpx>


As you see there are just 1 new attrbiute ``metadata/extensions/subtype`` (which is, of course, used for the subtype of the workout). The old ``trk/type`` attribute is now used to indicate the activity type of the workout. This implies that from now on, you'll have to always specify an ``metadata/extensions/subtype`` attribute.
