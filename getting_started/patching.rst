PATCHing
########

Because of a problem in our Load Balancer all the PATCH requests need to be handled in a special manner.

Anytime we mention in our API that you've to send a PATCH request, you have to send a POST request instead and specify the special X-HTTP-Method-Override.

For example, to update a user, this is the request in our docs:

**PATCH /user/[user_id]/**
**Content-Type: application/json**

::

    {
        "first_name": "John",
        "last_name": "Doe"
    }

The real request you have to do is this:

POST /user/[user_id]/
X-HTTP-Method-Override: PATCH
Content-Type: application/json
{
    "first_name": "John",
    "last_name": "Doe"
}


It's the same behavior but using a different approach.
