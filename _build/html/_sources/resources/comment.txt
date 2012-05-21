Comments
========

All posts in Athlete.com can have comments. This is the intention of this resource.

Create a comment
----------------

**POST /comment/**

Arguments

    :object_id: The id of the object this comment belongs to (e.g. post_id)
    :comment: The body of the comment.

Response

    201 CREATED. With a Location header indicating the URI of the resource.
