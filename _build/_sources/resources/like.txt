Likes
=====

Toggle a like
----------------

**POST /like/toggle/**

Arguments

    :object_type: The type of object being liked lowercase (e.g. comment, post)
    :object_id: The id of the object this comment belongs to (e.g. post_id)

Response

    Returns 200 OK with a document containing the current status of the object (liked by user, not liked by user) and the like count (total for that object).


Remove a like
-------------

Deletes the like for this user/object.

**DELETE /like/[object_type]/[object_id]**

Arguments - None

Response

    Nothing.
