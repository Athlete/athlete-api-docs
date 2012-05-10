Authentication
==============

.. _resource_login:

Login
-----

POST http://api.athlete.com/login

    :email: The user's email address (required)
    :password: The user's password (required)

Response
++++++++

:username: The user's username. This is different from their email.
:api_key: The api key for this user.


.. _resource_login_facebook:

Login with Facebook
-------------------

*Not implemented yet*

POST http://api.athlete.com/login_facebook

:token:
    The token received from Facebook. Must have been acquired using athlete.com's
    FB developer account. (required)

**Response**

:username: The user's username. This is different from their email.
:api_key: The api key for this user.


.. _resource_register:

Register
--------

*Not implemented yet*

POST http://api.athlete.com/register

:first_name: The user's first name (required)
:last_name: The user's last name (required)
:email: The user's email address (required)
:password: The user's password (required)

**Response**

:username: The user's username. This is different from their email.
:api_key: The api key for this user.


.. _resource_register_facebook:

Register with Facebook
----------------------

*Not implemented yet*

POST http://api.athlete.com/register_facebook

:token:
    The token received from Facebook. Must have been acquired using athlete.com's
    FB developer account. (required)

**Response**

:username: The user's username. This is different from their email.
:api_key: The api key for this user.

