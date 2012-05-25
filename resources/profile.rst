Profiles
========

Get a profile
-------------

**GET /profile/[profile_id]**

Example Response

::

    {
      "birth_date": "1983-05-17",
      "gender": "M",
      "id": 1,
      "resource_uri": "/api/v1/profile/1/",
      "user": "/api/v1/user/1/",
      "weight": "155",
      "weight_unit": "pounds"
    }


Update a profile
----------------

**PATCH /profile/[profile_id]/**

Arguments - A partial profile object, such as...

::

    {
        "gender": "M",
        "weight": 190,
        "weight_unit": "pounds"
    }

Response

    202 if successful. No response body.
    You are only permitted to update data for the current logged in user. If you try
    to update another user's profile, you'll get a 401 UNAUTHORIZED response.
