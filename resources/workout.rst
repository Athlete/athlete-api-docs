Workouts
========

Fetch all workouts for a user
-----------------------------

**GET /workout/**

    :user: The id of the user who's workouts you want

Response

    Not implemented yet. Needs to contain the following:

    - Static map image URL
    - Distance in meters
    - Duration in seconds
    - Run Type
    - Run title
    - Run date

    Also, if there is an associated Post then include the following data about that post:

    - Post body
    - Comment count
    - Like count


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
        :lon: The longitude
        :time: The date/time that this data point was recorded in ISO 8601 format
        :ele: The elevation at this data point (if available). Synonymous with altitude.

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
                "lon":"-111.5373066",
                "lat":"40.7231711",
                "time": "2012-01-01T00:00:04Z",
                "ele": "1942.1789265256325"
            },
            {
                "lon":"-111.5372056",
                "lat":"40.7228762",
                "time": "2012-01-01T00:00:07Z",
                "ele": "1942.109892409177"
            }
        ]
    }

Delete a workout
----------------

**DELETE /workout/[workout_id]/**

Response

    Not sure. Nothing of importance.
    You will get a 401 UNAUTHORIZED response if the current logged in user does not own the workout.
