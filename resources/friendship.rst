Friendships
===========

Friendships will always return accepted friendship, except for the current logged user. For the current logged user you can get a list of pending and accepted friendships.

Get friendships
-------------------

**GET /friendship/**

Arguments

    :none: No filters allowed.

Returns

    An list of the user's friendships. Each friendship resource will contain:

    - Information about the users involved
    - Information about the friendship (who's the requester, when the friendship was requested, etc.)


Get friends for particular user
-----------------------------------------

**GET /friendship/user/{id}/**

*Note: It may be more convient to get a list of friends (user objects), rather
than friendship objects. To get that, head on over to* :ref:`user_list`.

Arguments

    :status: If you're querying for the currently logged in user you can get a list of Pending or Accepted requests. (status=Accepted | status=Pending)

Returns

    An list of the user's accepted friendships. Each friendship resource will contain:

    - Information about the users involved
    - Information about the friendship (who's the requester, when the friendship was requested, etc.)


Request friendship
------------------

**POST /friendship/request/**

Arguments

    :user_id: The id of the user who's frienship is being requested. The requester is always the logged in user.

Returns

    The friendship object if it was created. If the object already existed, you'll get an error response.


Cancel friendship request, Remove friend
----------------------------------------

In either case you are essentially deleting any record of association between these two users.

**DELETE /friendship/[friendship_id]/**

Response

    No content.


Accept a friend request
-------------------------------

**POST /friendship/accept/**

If the logged in user is not the requester of that friendship, you'll get a 401 UNAUTHORIZED response.

Arguments

    :friendship_id: The id of the friendship to accept

Response

    An object representing the details of the friendship.

Search for friends
-------------------

Please see :ref:`resources/user` for more information.
