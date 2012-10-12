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

Please see :ref:`user` for more information.


Invite a friend by email
------------------------

**POST /invitation/**

Arguments

    :email: The email of the person to invite.
    :name: (optinal) The name of the person to invite.

Response

    200 If successful
 
This will create an invitation in our system to track that current logged in user sent an invite to this email address.
If/when the receiving user registers with athlete.com, they will automatically be made friends with the person that
invited them. If the receiving user is already an athlete.com user, a regular friendship request will be created instead.


Friendship exists for a user
----------------------------

**GET /friendship/exists/{id}/**

This is a method to query if a given user (U1) is friend of other user (U2). To make this method work you need to provide the correct GET argument.

Arguments

    :with_user_id: The other user to check friendship.
    :status: If the user provided is the same as the logged in user, you can query for pending requests.

Returns

    The friendship object if exists. 404 in other case.

Example:

If I have the user id 12 and I want to check if that user is friend of user id 83. I can issue this request:

    GET /api/v1/friendship/exists/12/?with_user_id=83

It also works backward:

    GET /api/v1/friendship/exists/83/?with_user_id=12

If your logged in user is, for example, the user 12, you can ask if the friendship is pending:

    GET /api/v1/friendship/exists/12/?with_user_id=83&status=Pending
