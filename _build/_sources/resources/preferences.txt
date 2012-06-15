Preferences
===========

.. _resource_preferences_get:

Get preferences
---------------

**GET /preferences/[preferences_id]/**

Example Response

::

    {
      "annually_email_report": true,
      "distance": "miles",
      "elevation": "feet",
      "id": 1,
      "monthly_email_report": true,
      "resource_uri": "/api/v1/preferences/1/",
      "timezone": "UTC",
      "user": "/api/v1/user/1/",
      "weekly_email_report": true
    }


Update Preferences
------------------

**PATCH /preferences/[preferences_id]/**

Arguments - A partial preferences object, such as...

::

    {
        "distance": "miles",
        "elevation": "feet"
    }

Response

    202 if successful. No response body.
    You are only permitted to update data for the current logged in user. If you try
    to update another user's preferences, you'll get a 401 UNAUTHORIZED response.

Same as `Get preferences` response, except only the ones you are updating.
