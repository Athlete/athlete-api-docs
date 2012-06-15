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


.. _resource_login_facebook:

Login or Register with Facebook
-------------------------------

**POST /account/facebook/login/**

This will either login or register the user, depending on if the user is already
registered. If ther user is already registered, but not through facebook, it will
attempt to match the account by email and link the facebook id to this account.
So it pretty must just always works no matter what. Give it a token and the user
will be ready to go.

Arguments

    :token:
        The token received from Facebook. Must have been acquired using athlete.com's
        FB developer account. (required)
        **IMPORTANT: The token granted from facebook must have the "email", "user_birthday" and
        "user_photos" privileges.**

Response

    :username: The user's username. This is different from their email.
    :api_key: The api key for this user.
    :created: True if the user was created, False if it was an existing user who was just logged in.


Forgot password
---------------

**POST /account/forgot_password**

Arguments

    :email: The email address of the account for which the password should be reset (required)

Response

    An email will be sent to the email address specified providing further instructions for changing the
    password. The response will be a 200 response if successful.
    
    If the email address is not found in our system you'll get a 400 response with a 109 error code.
