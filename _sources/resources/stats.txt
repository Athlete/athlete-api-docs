Stats
=====

This is a read-only resource that gets automatically updated whenever a user's stats change (e.g. when they log a run).
Think of it as a cache.

Get stats for a user
--------------------

**GET /stats/[stats_id]/**

Response

    200 OK. You'll get a response body that looks like this:

::

    {
      "avg_weekly_distance_in_meters": 0,
      "best_10k_duration_in_seconds": 2763,
      "best_5k_duration_in_seconds": 1226,
      "best_half_marathon_duration_in_seconds": null,
      "best_marathon_duration_in_seconds": null,
      "best_mile_duration_in_seconds": 343,
      "id": 1,
      "latest_workout_date": "2012-07-03T17:00:00",
      "max_distance_in_meters": "10408.85",
      "max_duration_in_seconds": 2908,
      "max_elevation_gain_in_meters": "300.09",
      "resource_uri": "/api/v1/stats/1/",
      "total_distance_in_meters": 10408,
      "user": "/api/v1/user/1/"
    }
