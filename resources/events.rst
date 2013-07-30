Events
========

Get an Event resource
-----------------------------

**GET /event/:event_id**

Response

::

    {
      "end_date": "2013-06-30T00:00:00",
      "home_url": "http://test.athlete.com/events/4/one-run-for-boston",
      "id": 4,
      "info_url": "http://test.athlete.com/events/4/one-run-for-boston/promo",
      "name": "One Run For Boston",
      "resource_uri": "/api/v1/event/4/",
      "start_date": "2013-06-01T00:00:00"
    }

Something to note

    :start_date and end_date: These both datetimes are not UTC. Instead, they're based on the user's timezone. Using datetime slang: these two are naive datetimes that must be made aware to the user's timezone.

Event Particiapnts
-----------------------------

Event participant is the abstraction created to represent a certain user that is participating in certain event. You already have some information about a particular event (se above). In this case, you will have a detail of the user participating in that event, with useful information. Here's an example:

::

    {
      "id": 328,
      "resource_uri": "/api/v1/event-participant/328/",
      "description": "I run to support this cause",
      "participant_url": "https://test.athlete.com/events/participant/328/Santiago+Basulto",

      "total_miles_logged": 23,
      "active": true,
      "amount_per_mile": 0.5,
      "user_goal_in_miles": 11,

      "event": {
        "end_date": "2013-06-30T00:00:00",
        "home_url": "http://test.athlete.com/events/4/one-run-for-boston",
        "id": 4,
        "info_url": "http://test.athlete.com/events/4/one-run-for-boston/promo",
        "name": "One Run For Boston",
        "resource_uri": "/api/v1/event/4/",
        "start_date": "2013-06-01T00:00:00"
      },
      "user": {
        "email": "sanbasulto_04@hotmail.com",
        "first_name": "Santiago",
        "id": 11,
        "last_name": "Basulto",
        "preferences": "/api/v1/preferences/11/",
        "profile": "/api/v1/profile/11/",
        "profile_image_225_url": "http://com-athlete-testing-profile-images.s3.amazonaws.com/55/7ba30e2340c692647d206b7b955499/perfil.jpg",
        "profile_image_48_url": "http://com-athlete-testing-profile-images.s3.amazonaws.com/3e/4cfd176efe1dad173f4e33d81cc570/perfil.jpg",
        "resource_uri": "/api/v1/user/11/",
        "stats": "/api/v1/stats/11/"
      }
    }

The most important data here (I won't detail info about Event and User, refer to the docs for each resource):

    :active: IMPORTANT! This field indicates if the event is still undergoin for this user. This means if this is True, then all workouts uploaded by this user will count toward this event.
    :description: This is the description the user gave about his participation in this event.
    :participant_url: This is the full web participant URL.
    :total_miles_logged: Total miles logged by this participant (ran, walked, cycled).
    :amount_per_mile: This is the amount of money raised by this user for this event. Each mile the user runs, he'll get this value in money for the cause he's running for. You can use this value (and total_miles_logged) to compute the total money raised by this user at this point in time.
    :user_goal_in_miles: This is the user's goal for this event. This is set by the user and as the name implies, it's in miles.

Some of the most prominent resources bellow:

**GET /event-participant/**

This is the EventParticipant Resource endpoint. More following.

**GET /event-participant/?user_id=:user_id**

Get All event participants for the user with ID :user_id. Not really useful because contains all active and unactive events participants.

**GET /event-participant/?user_id=:user_id**

Get All event participants for the user with ID :user_id. Not really useful because contains all active and unactive events participants.

Hotness
-------

This is the name we've gave to the "hot" participations for a given user. If you ask for hot participants for a given user you'll get:

* Active participants. I.e: Events currently active in which the user is participating in.
* Events finished less than a week ago: The event is already done, the event participant is no longer active. But it's still hot. Of course, if the user uploads a workout, it doesn't have to count toward this event.
* All future event participants: The user is already registered for an event that has not yet started. The event participant is NOT active. Same rule than before. But you might want to show it to her/him.

To query for this EventParticipants you must use the ``status`` attribute with the ``hot`` value. This is an example to query for all hot event participants for a given user:

**GET /event-participant/?user_id=:user_id&status=hot**

You'll get something like:

::

    {
      "meta": {
        "limit": 20,
        "next": null,
        "offset": 0,
        "previous": null,
        "total_count": 2
      },
      "objects": [
        {
          "active": false,
          "amount_per_mile": 0.5,
          "description": "I run because I love it",
          "event": {
            "end_date": "2013-06-30T00:00:00",
            "home_url": "http://test.athlete.com/events/4/one-run-for-boston",
            "id": 4,
            "info_url": "http://test.athlete.com/events/4/one-run-for-boston/promo",
            "name": "One Run For Boston",
            "resource_uri": "/api/v1/event/4/",
            "start_date": "2013-06-01T00:00:00"
          },
          "id": 328,
          "participant_url": "https://test.athlete.com/events/participant/328/Santiago+Basulto",
          "resource_uri": "/api/v1/event-participant/328/",
          "total_miles_logged": 23,
          "user": {
            "email": "sanbasulto_04@hotmail.com",
            "first_name": "Santiago",
            "id": 11,
            "last_name": "Basulto",
            "preferences": "/api/v1/preferences/11/",
            "profile": "/api/v1/profile/11/",
            "profile_image_225_url": "http://com-athlete-testing-profile-images.s3.amazonaws.com/55/7ba30e2340c692647d206b7b955499/perfil.jpg",
            "profile_image_48_url": "http://com-athlete-testing-profile-images.s3.amazonaws.com/3e/4cfd176efe1dad173f4e33d81cc570/perfil.jpg",
            "resource_uri": "/api/v1/user/11/",
            "stats": "/api/v1/stats/11/"
          },
          "user_goal_in_miles": 11
        },
        {
          "active": false,
          "amount_per_mile": 0,
          "description": "",
          "event": {
            "end_date": "2013-06-30T00:00:00",
            "home_url": "http://test.athlete.com/events/5/run-a-mile-for-a-special-child",
            "id": 5,
            "info_url": "http://test.athlete.com/events/5/run-a-mile-for-a-special-child/promo",
            "name": "Run a Mile for a Special Child",
            "resource_uri": "/api/v1/event/5/",
            "start_date": "2013-06-01T00:00:00"
          },
          "id": 335,
          "participant_url": "https://test.athlete.com/events/participant/335/Santiago+Basulto",
          "resource_uri": "/api/v1/event-participant/335/",
          "total_miles_logged": 23,
          "user": {
            "email": "sanbasulto_04@hotmail.com",
            "first_name": "Santiago",
            "id": 11,
            "last_name": "Basulto",
            "preferences": "/api/v1/preferences/11/",
            "profile": "/api/v1/profile/11/",
            "profile_image_225_url": "http://com-athlete-testing-profile-images.s3.amazonaws.com/55/7ba30e2340c692647d206b7b955499/perfil.jpg",
            "profile_image_48_url": "http://com-athlete-testing-profile-images.s3.amazonaws.com/3e/4cfd176efe1dad173f4e33d81cc570/perfil.jpg",
            "resource_uri": "/api/v1/user/11/",
            "stats": "/api/v1/stats/11/"
          },
          "user_goal_in_miles": 0
        }
      ]
    }
