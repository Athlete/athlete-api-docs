Authentication
==============

.. _resource_login:

Login
-----

**POST /account/login/**

Arguments

    :email: The user's email address (required)
    :password: The user's password (required)

Response

    :username: The user's username. This is different from their email.
    :api_key: The api key for this user.


.. _resource_login_facebook:

Login with Facebook
-------------------

**POST /account/facebook/login/**

Arguments

    :token:
        The token received from Facebook. Must have been acquired using athlete.com's
        FB developer account. (required)
        **IMPORTANT: The token granted from facebook must have the "email", "user_birthday" and
        "user_photos" privileges.**

Response

    :username: The user's username. This is different from their email.
    :api_key: The api key for this user.


.. _resource_register:

Register
--------

**POST /account/register/**

Arguments

    :first_name: The user's first name (required)
    :last_name: The user's last name (required)
    :email: The user's email address (required)
    :password: The user's password (required)

Response

    :username: The user's username. This is different from their email.
    :api_key: The api key for this user.

If a user already exists with the provided email address, the response will have a 400
status code and the body will say ``The email address already exists``.


.. _resource_register_facebook:

Register with Facebook
----------------------

**POST /account/facebook/register/**

Arguments

    :token:
        The token received from Facebook. Must have been acquired using athlete.com's
        FB developer account. (required)
        **IMPORTANT: The token granted from facebook must have the "email", "user_birthday" and
        "user_photos" privileges.**

Response

    :username: The user's username. This is different from their email.
    :api_key: The api key for this user.

If an account already exists with the email address we receive from Facebook, the accounts will
be automatically merged without an error.

Forgot password
---------------

**POST /account/forgot_password**

Arguments

    :email: The email address of the account for which the password should be reset (required)

Response

    An email will be sent to the email address specified providing further instructions for changing the
    password. The response will be a 200 response if successful. You will get a non 200 response and possibly
    and error message in the reponse body if the email failed to send or there is no user found with that email.
