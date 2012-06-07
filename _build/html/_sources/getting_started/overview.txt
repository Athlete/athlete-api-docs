Overview
########

Our API is built using TastyPie. We will explain pretty much everything you need to know in our
docs, but you might find it useful to know a little bit more under the hood how things work.

http://django-tastypie.readthedocs.org/en/latest/

Documentation Format
--------------------

Each API method you can call is in the following format:

    [METHOD] [PATH]
    
    Arguments
    
        :[ARG1]: [DESCRIPTION] (required)
        :[ARG2]: [DESCRIPTION]
    
    Response
    
        :[ARG1]: [DESCRIPTION]

Where METHOD is POST/GET/PUT...
and PATH is the path relative to the endpoint.

- For production, the endpoint is http://beta.athlete.com/api/v1
- For testing, the endpoint is http://staging.athlete.com/api/v1

So if PATH is /user/1/, the full URL for testing would be
http://staging.athlete.com/api/v1/user/1/


Request Format
---------------

You MUST specify the content type in your requests (eg: Content-Type: application/json). Currently, we support several formats (json, xml, yaml, formdata) but the prefered one is json. There are simple
methods that doesn't need much data, like the login method. In that case you can use formdata format (param1=data1&param2=data2). Example:

    POST /account/login
    Content-Type: application/x-www-form-urlencoded
    email=test@athlete.com&password=123

Response Format
---------------

Response format can be dictated by the Accepts header or by putting format=[xml|json|...] in the query
string. See `tastypie docs <http://django-tastypie.readthedocs.org/en/latest/interacting.html#front-matter>`_
for more information.

Status codes are used properly. If you get a 200 repsonse, you can expect the normal response body as
documented. Otherwise the response body will contain a plain text error message, or sometiemes no message.

For example, if you don't include the Authorization header, you will get a 401 UNAUTHORIZED status
code and no response body.


Standard Response Fields
------------------------

All or nearly all objects returned in some response will have a resource URI. This is the URI you can use
to fetch details for this object. For example, if you fetch a user object, it will have an attribute
called preferences which is a resource URI for the preferences for that user. The user object itself will
also have an attribute call resource_uri.


Units
-----

- Distances and elevations will always be in meters.
- Weights will always be in kilograms, except the user's weight can either be in lbs or kgs, as specified by the weight_unit attribute.
- Durations will always be in seconds.
- Timestamps will always be in ISO 8601 format (e.g. '2012-05-14T17:54:16.521019'). Unix Epochs are convenient, but are
  not the web standard. Timestamps from the API will always be UTC.

Use :ref:`resource_preferences_get` to get the user's distance and elevation unit preference.
