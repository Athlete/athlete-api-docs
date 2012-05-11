Authentication
==============

.. _resource_login:

Login
-----

**POST /account/login**

Arguments

    :email: The user's email address (required)
    :password: The user's password (required)

Response

    :username: The user's username. This is different from their email.
    :api_key: The api key for this user.


.. _resource_login_facebook:

Login with Facebook
-------------------

**POST /account/facebook/login**

Arguments

    :fb_user_id:
        The Facebook user ID provided by facebook.

Response

    :username: The user's username. This is different from their email.
    :api_key: The api key for this user.


.. _resource_register:

Register
--------

*Not implemented yet*

**POST /account/register**

Arguments

    :first_name: The user's first name (required)
    :last_name: The user's last name (required)
    :email: The user's email address (required)
    :password: The user's password (required)

Response

    :username: The user's username. This is different from their email.
    :api_key: The api key for this user.


.. _resource_register_facebook:

Register with Facebook
----------------------

*Not implemented yet*

**POST /account/register/facebook**

Arguments

    :token:
        The token received from Facebook. Must have been acquired using athlete.com's
        FB developer account. (required)

Response

    :username: The user's username. This is different from their email.
    :api_key: The api key for this user.

