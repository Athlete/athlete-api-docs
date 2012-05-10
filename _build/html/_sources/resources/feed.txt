Feed
====

**GET /feed/**

Arguments

    :limit: Max feed items to return (default=20)
    :offset: Feed item index to start with (default=0)

Example Response

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
