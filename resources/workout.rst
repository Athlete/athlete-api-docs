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

Note that workouts (and posts) can also have attached images. Those must be posted separately

    :user: The id for the user that owns this workout (we might omit this argument and just use the logged in user)
    :run_date: A DateTime in format ISO 8601 format
    :title: The run title (whatever the user wants to call this run)
    :run_type: Must be one of Endurance, Tempo, Slow, Interval, Group, Elevation, Race
    :duration_in_seconds: The duration of the run, in seconds. If the user paused during that run, that time should not be included.
    :distance_in_meters: The distance of the run in meters.
    :points: An optional array of objects, each containing the following attributes:
        :lat: The latitude
        :lng: The longitude
        :timestamp: The date/time that this data point was recorded in ISO 8601 format
        :elevation: The elevation at this data point (if available). Synonymous with altitude.


Delete a workout
----------------

**DELETE /workout/[workout_id]/**

Response

    Not sure. Nothing of importance.
    You will get a 401 UNAUTHORIZED response if the current logged in user does not own the workout.
