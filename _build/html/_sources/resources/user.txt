Users
=====

Fetch a single user
-------------------

**GET /user/[user_id]/**

You can also get the current authenticated user with

**GET /me/**

Arguments - None

Example Response

::

    {
      "date_joined": "2012-05-01T11:37:52.467275",
      "first_name": "Dustin",
      "id": 1,
      "last_name": "McQuay",
      "preferences": "/api/v1/preferences/1/",
      "profile": "/api/v1/profile/1/",
      "resource_uri": "/api/v1/user/1/",
      "profile_image_225_url": "https://s3.amazonaws.com/com.athlete.profiles.development/test1/a4018714-ac33-4bd8-8ed2-f79286e31a87/var/folders/kq/mc4mjdx5797d1cc_g0x7y8n00000gn/T/tmpmMOvsp?Signature=MP4mYdL40xHb8koO4j04XbYUjNA%3D&Expires=1652635711&AWSAccessKeyId=AKIAIPH52TGT42OHQBPQ",
      "profile_image_48_url": "https://s3.amazonaws.com/com.athlete.profiles.development/test1/aabe95d7-d127-458f-8205-720eb2a16c35/var/folders/kq/mc4mjdx5797d1cc_g0x7y8n00000gn/T/tmpW_XuLr?Signature=cpGdaEQzyimEFMAq9GWNu%2BxI3m4%3D&Expires=1652635712&AWSAccessKeyId=AKIAIPH52TGT42OHQBPQ"
    }

*Note: we will be adding profile image URLs to this response soon.*


Search users by name
--------------------

**GET /user/**

Arguments

    :name: The name to match against in the search

Response

    TBD - Must include profile pic URL, name and location.


Update a user
-------------

**PATCH /user/[user_id]/**

Arguments - A partial user object, such as...

::

    {
        "first_name": "John",
        "last_name": "Doe"
    }

Response

    202 if successful. No response body.
    You are only permitted to update data for the current logged in user. If you try
    to update another user, you'll get a 401 UNAUTHORIZED response.
