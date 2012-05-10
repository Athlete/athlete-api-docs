Overview
########

Our API is built using TastyPie. We will explain pretty much everything you need to know in our
docs, but you might find it useful to know a little bit more under the hood how things work.

http://django-tastypie.readthedocs.org/en/latest/

Response Format
---------------

Response format can be dictated by the Accepts header or by putting format=[xml|json|...] in the query
string.

Status codes are used properly. If you get a 200 repsonse, you can expect the normal response body as
documented. Otherwise the response body will contain a plain text error message, or sometiemes no message.

For example, if you don't include the Authorization header, you will get a 401 UNAUTHORIZED status
code and no response body.
