Authentication
==============

There are two levels of authentication involved in every API call.

1. User
2. Client

Let's say you are making a mobile app. Your app is the Client. The user who is using your app is the User.

Client Authentication
---------------------

For client authentication, you will need a public/private key pair which you will get from us (the Athlete.com
developers). We don't have an automated way to get this yet. You will use these keys in every request. The
public key will be included in the request as a query parameter. The private key will be used to create a signature.
The signature will also be added to the request as a query parameter. The private key is not included (intentionally).
You need to keep this one secret.

Over time we will hopefully provide libraries in various languages that take care of the request signing for you, but
for now you'll need to implement it yourself. I will document here exactly how that request signing must work.

Basically you need to do the following

#. Add the following parameters to the query string:
    #. The current UTC time in ISO 8601 format (e.g. 'timestamp=2012-05-14T17:54:16.521019')
    #. The public key (e.g. 'public_key=abcdefg12345')
#. Create a string that represents the entire request. It should contain the following, in order, separated by a unix-style newline character.
    #. Request Method (e.g. GET, POST, PUT). Must be uppercase.
    #. Path. This is the URL minus the protocol, domain and port. (e.g. /api/v1/users/)
    #. All GET parameters, sorted by key and serialized in querystring format (e.g. a=b&c=d). Each key/value
       must be urlencoded consistent with `python's urllib.quote <http://docs.python.org/library/urllib.html#urllib.quote>`_.
       This includes the two you just added above (timestamp and public_key).
    
    *Note: We may add the body of the request to this at some point in the future. We haven't figured out exactly how
    we want to handle that yet. For now it is NOT included.*
#. Sign that string and add that signature to the query string.
    The string that you are signing should now look something like this:
    ``GET\n/api/v1/user/\npublic_key=123&timestamp=2012-05-14T18%3A20%3A38.610086``
    
    #. Create a SHA256 HMAC digest using the private key and the above string as the message.
    #. Base64 encode that digest and add it to the query string parameters (e.g. 'signature=n3UG0g6xwaFVy8qtk4AUnXGEHocWOlQkkmFzTVJlXbk%3D')

The signed request will become invalid in any of the following circumstances:

- If the timestamp is too old or too new (a signed request is only valid for about 5 minutes)
- If any of the parameters are changed without creating a new signature
- If the request method or URI are changed without creating a new signature
- If the private key is changed on our servers.
    - This is useful in the case that your private key is compromised. Just ask us to create a new one for
      you and your old one will stop working.
    - If you are abusing our service, we may also change your key to revoke your access to the API.


User Authentication
-------------------

Client authentication gets you access to the API generally, but you are generally accessing data on behalf of a user
and therefore you need permission to do so. We do this using a username and an api key.

You can obtain a username and api key for a new or existing user with one of the following:

- :ref:`resource_login`
- :ref:`resource_login_facebook`
- :ref:`resource_register`
- :ref:`resource_register_facebook`

Once you have the username and api key, you'll put it in the Authorization header of every request. It should look like this:

    Authorization: ApiKey <username>:<api_key>

Read the `Tastypie ApiKey Authentication docs <http://django-tastypie.readthedocs.org/en/latest/authentication_authorization.html#apikeyauthentication>`_ for more information.
