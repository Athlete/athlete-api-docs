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


.. _user_list:

Fetch multiple users
--------------------

**GET /user/**

    :friends_with: Return only users who are friends with this user (user_id)

Response

    A list of user objects which are formatted just like the Example Response for
    fetching a single user.


Search users by name
--------------------

**GET /user/search/**

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


Change profile picture
----------------------

This resource is exposed in order to change the profile picture of the current logged in user. [PRE PROCESSING NOTES]

**POST /user/profile/**

Arguments

The entire content of the request (i.e. the request body) must contain the content of the image that you want to upload. You just need to open the file, read the contents, and place them in the request body.

There are some **headers** you might need to send. Some are optionals, other are required.:

    Content-MD5 (OPTIONAL): Is the result of aplying MD5 digest on the content you're sending. Based on http://www.ietf.org/rfc/rfc1864.txt It's important to note that this method is highly used in a wide variety of APIs, being a well known one S3 from Amazon. If you have doubt on how implement this, you can browse some opensource library for S3 and you can find a good example.
    Content-Type (REQUIRED): This is the content type of the picture you're sending. Right now the only content types supported are: "image/jpeg" and "image/png"
