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

#. Add a timestamp parameter to the query string. This should be UTC time in ISO 8601 format.
#. Add the public key to the query string. (e.g. public_key=...)
#. Create a string with the following contents separated by unix style newlines (\n)
    #. Request Method (e.g. GET, POST, PUT). Not case sensitive.
    #. URI or Path. The URL minus the protocol, domain and port. (e.g. /api/v1/users/)
    #. All GET and POST parameters, sorted by key and serialized in querystring format (e.g. a=b&c=d). Each key/value
       must be urlencoded consistent with python's urllib.quote.
#. Create a SHA256 HMAC digest using the private key and the above string as the message.
#. Base64 encode that digest and add it to the querystring parameters as the 'signature' parameter (e.g. ...&signature=...)

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

Before you can do any requests on the user's behalf, you need to collect the user's email and password. You'll
send that to our login API method and will receive the users's username and api key which you will then send in the
Authorization header of every API request.

As I just stated, you will collect the user's username and password. But you must not store it. You will use it to
obtain the user's username and api key and then you will no longer need it.

The authorization header is formatted like this:

    Authorization: ApiKey <username>:<api_key>
