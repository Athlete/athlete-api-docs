Friendships
===========

Get friends for user
--------------------

**GET /user/[user_id]/friends/**

Arguments

    :status: Pending, Accepted or ALL. (optional, default=Accepted)

Returns

    An list of the user's friends. Each friend object will contain:

    - Profile image URL
    - Full Name
    - User ID
    - User Resource URL


Request friendship
------------------

**POST /friendship/**

Arguments

    :user: The id of the user who's frienship is being requested. The requester is always the logged in user.

Returns

    The friendship object if it was created. If the object already existed, you'll get an error response.


Cancel friendship request, Remove friend
----------------------------------------

In either case you are essentially deleting any record of association between these two users.

**DELETE /friendship/[user_id]/[user_id]/**

The leftmost user_id in the url should be the alphanumerically lowest id. However, it will work either way.

Response

    Not sure yet. Nothing important to return.


Accept or deny a friend request
-------------------------------

**PATCH /friendship/[user_id]/[user_id]/**

If the requestee is not the current logged in user, you'll get a 401 UNAUTHORIZED response.

Arguments

    :status: Pending or Accepted

Response

    An object representing the details of the friendship.
