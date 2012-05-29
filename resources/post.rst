Posts (a.k.a. Feed)
===================

Get One Post
------------

**GET /post/[id]/**

Arguments - None

Example Response

::

    {
      "author": {
        "first_name": "Dustin",
        "id": 1,
        "last_name": "McQuay",
        "preferences": "/api/v1/preferences/1/",
        "profile": "/api/v1/profile/1/",
        "resource_uri": "/api/v1/user/1/"
      },
      "body": "What a great run!",
      "comment_count": 0,
      "created_date": "2012-05-17T11:31:22.492757",
      "id": 3,
      "likers": [1, 2],
      "resource_uri": "/api/v1/post/3/",
      "workout": {
        "distance_in_meters": "3862.43",
        "duration_in_seconds": 1380,
        "id": 2,
        "resource_uri": "/api/v1/workout/2/",
        "run_date": "2012-05-17T00:00:00",
        "run_type": "Interval",
        "title": "Running"
      }
    }


Get List of Posts
-----------------

**GET /post/**

Arguments

    :type: [dashboard|local|featured|profile] A special filter to get posts for a user's dashboard, local posts, featured posts or the profile feed posts.
    :user_id: Only valid when type is dashboard. Specifies the id of the user who's dashboard posts should be returned.
    :limit: Max feed items to return (default=20)
    :offset: Feed item index to start with (default=0)

Response

    You'll get a list of post objects. It will be paginated.
    
    It is very possible that the user specified has provided a location in their settings that we were unable to resolve
    to get a latitude and longitude. Without that, we cannot determine who is "local" to them. In this case you will get
    a normal response with 0 results.

Example Response

::

    {
      "meta": {
        "limit": 20,
        "next": null,
        "offset": 0,
        "previous": null,
        "total_count": 3
      },
      "objects": [
        {
          "author": {
            "first_name": "Dustin",
            "id": 1,
            "last_name": "McQuay",
            "preferences": "/api/v1/preferences/1/",
            "profile": "/api/v1/profile/1/",
            "resource_uri": "/api/v1/user/1/"
          },
          "body": "What a great run!",
          "comment_count": 0,
          "created_date": "2012-05-17T11:31:22.492757",
          "id": 3,
          "likers": [
            1
          ],
          "resource_uri": "/api/v1/post/3/",
          "workout": {
            "distance_in_meters": "3862.43",
            "duration_in_seconds": 1380,
            "id": 2,
            "resource_uri": "/api/v1/workout/2/",
            "run_date": "2012-05-17T00:00:00",
            "run_type": "Interval",
            "title": "Running"
          }
        },
        {
          "author": {
            "first_name": "Dustin",
            "id": 1,
            "last_name": "McQuay",
            "preferences": "/api/v1/preferences/1/",
            "profile": "/api/v1/profile/1/",
            "resource_uri": "/api/v1/user/1/"
          },
          "body": "",
          "comment_count": 0,
          "created_date": "2012-05-17T11:30:35.241416",
          "id": 2,
          "likers": [
            1
          ],
          "resource_uri": "/api/v1/post/2/",
          "workout": {
            "distance_in_meters": null,
            "duration_in_seconds": 3600,
            "id": 1,
            "resource_uri": "/api/v1/workout/1/",
            "run_date": "2012-05-17T00:00:00",
            "run_type": "Endurance",
            "title": "Running"
          }
        }
      ]
    }

