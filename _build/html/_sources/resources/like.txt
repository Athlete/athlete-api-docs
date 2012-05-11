Likes
=====

Create a like
----------------

Note: only one like per object per user is allowed.

**POST /like/**

Arguments

    :object_type: The type of object being liked (e.g. comment, post)
    :object_id: The id of the object this comment belongs to (e.g. post_id)

Response

    Not implemented. Will probably be an updated like count for the object.


Remove a like
-------------

Deletes the like for this user/object.

**DELETE /like/[object_type]/[object_id]**

Arguments - None

Response

    Not implemented. Nothing of importance to be returned though.
