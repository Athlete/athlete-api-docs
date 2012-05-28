Comments
========

All posts in Athlete.com can have comments. This is the intention of this resource.

Create a comment
----------------

**POST /comment/**

Arguments

    :post_id: The id of the post this comment belongs to.
    :comment: The body of the comment.

Response

    201 CREATED. With a Location header indicating the URI of the resource.

Get a comment
----------------

**GET /comment/[comment_id]/**

Arguments

    :comment_id: The id of the comment you want to get.

Response

    200 OK. Comment on response body.

Delete a comment
----------------

**DELETE /comment/[comment_id]/**

Arguments

    :comment_id: The id of the comment you want to get. Is important to note that you user can delete his/her own comments and comments that belong to him or her. If you make an attempt to remove a comment that is beyond you're user scope, a 404 will be returned.

Response

    204 OK. No content.
