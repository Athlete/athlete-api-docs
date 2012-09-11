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

Specifying a location
---------------------

The fields to specify a location are these:

    :location_name: The name of the location
    :location_lat: The Latitude of the location
    :location_lng: The Longitude of the location

You should always try to verify that data with your user and provide a right location.

If you only have a location_name, we will make our best effort to get good latitude and longitude information. It means we'll try to get lat and lon from that name.

If you only provide location_lat and location_lng we'll try to get the name of that location.

Please note that both methods describe above (just name, or just lat and lng) are not always precise. The user experience might be affected by this.
