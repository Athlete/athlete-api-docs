Users
=====

Fetch a single user
-------------------

**GET /user/[user_id]/**

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
      "resource_uri": "/api/v1/user/1/"
    }

The following fields will be added to this response. It's on my To Do list.

- gender
- birday
- distance preference
- weight preference
- weight
- image urls


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
