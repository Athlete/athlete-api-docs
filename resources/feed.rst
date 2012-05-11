Feed
====

Friends' Feed
-------------

This feed shows all activity/posts for all of the authenticated user's friends.
It also includes activity/posts for the current logged in user.

**GET /feed/friends/**

Arguments

    :limit: Max feed items to return (default=20)
    :offset: Feed item index to start with (default=0)

Example Response

*Note:* The following data is missing from this response and will be added:

- Author name
- Author profile image URL
- Workout (if there is an associated workout) with the following data:
    - Distance in meters (can be null)
    - Duration in meters (can be null)
    - Pace (can be null)
    - Run Type

::

    {
      "meta": {
        "limit": 2,
        "next": null,
        "offset": 1,
        "previous": null,
        "total_count": 36
      },
      "objects": [
        {
          "body": "",
          "comment_count": 0,
          "created_date": "2012-05-10T10:09:10",
          "distance": 32186.8800122938,
          "duration": 1200,
          "id": 98,
          "like_count": 0,
          "resource_uri": "",
          "run_date": "2012-05-10T10:09:10",
          "run_title": "Running",
          "run_type": "Endurance"
        },
        {
          "body": "",
          "comment_count": 0,
          "created_date": "2012-05-10T06:30:39",
          "distance": 8046.72000307346,
          "duration": 600,
          "id": 97,
          "like_count": 0,
          "resource_uri": "",
          "run_date": "2012-05-10T06:30:39",
          "run_title": "R",
          "run_type": "Endurance"
        }
      ]
    }


Profile Feed
------------

Shows only activity/posts for the specified user.

**GET /feed/profile/[user_id]/**

Arguments and example response are the same as `Friends' Feed`_.


Local Feed
----------

Shows activity/posts for all users within 200 miles of the current logged in user. This is done
according to the location that the user specified in their settings.

**GET /feed/local/**

Arguments and example response are the same as `Friends' Feed`_.


Featured Feed
-------------

Shows activity/posts for featured users.

**GET /feed/featured/**

Arguments and example response are the same as `Friends' Feed`_.
