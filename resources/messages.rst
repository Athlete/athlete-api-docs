Conversations
==============

A user might be involved in a conversation. You can only fetch the conversations that your user is involved in. You might want to display information to your user informing the status of the conversations (read/unread). It's important to mark the conversation as read when you your user reads it.

Get Conversations for Inbox
---------------------------

**GET /conversation/inbox/**

Arguments - None

Returns all the conversations for the current user's inbox, sorted by last active.
Results are paginated.

Get Conversations for Archive
-----------------------------

**GET /conversation/archive/**

Arguments - None

Returns the current user's archived messages, sorted by last active. Results are paginated.

Get One Conversation
---------------------

**GET /conversation/[id]/**

You get some important fields:
    :has_unread_messages: shows if the currently logged in user have read all messages (true, false).
    :last_message: The last message from this conversation.
    :created_date: Date created this conversation.
    :recipients: A list of users, with all their information.
    :started_by: The user that started the conversation.
    :past_users_involved: A list of names of users that participated in this conversation but deleted their accounts.

Mark conversations as read
---------------------------

We don't mark conversation as read when you fetch the messages for that particular conversation. This is really important. You have to explicitly inform us when the user has read the conversation. To do so, you must issue this request:

**POST /conversation/[ID]/read/**

Arguments

    :last_message_id: The ID of the last message in this conversation you have read

last_message_id is used to check if any new messages have been added to this conversation since you last fetched them, so you don't falsely mark this conversation as read when
there are in fact messages in the conversation you have not yet seen.

Response

    :200 Ok: if there are no new messages since the time you informed. You can safetly inform your user that he/she has read the conversation.
    :409 CONFLICT: New messages have been created. At this point you can fetch the messages again and reissue this request.

Get One Conversation
---------------------

**GET /conversation/[id]/**

You get some important fields:
    :has_unread_messages: shows if the currently logged in user have read all messages (true, false).
    :last_message: The last message from this conversation.
    :created_date: Date created this conversation.
    :recipients: A list of users, with all their information.
    :started_by: The user that started the conversation.


Start a new Conversation
-------------------------

**POST /conversation/**

To create a new conversation you must provide the message and a list of id of the users recipients, this is an example:

Arguments:

    {"message" : "This is the first message", "recipients" : [17,32, 1090]}

Response:

You get the Location header with the URI for the recently created resource.

    Location: https://athlete.com/api/v1/conversation/[ID]/

Archive a Conversation
----------------------

**PATCH /conversation/[id]/archive/**

There is no response. This conversation will no longer show up in the current user's inbox,
but it will show in their archive. It will also be searchable.

Hide a Conversation
---------------------

**PATCH /conversation/[id]/hide/**

There is no response. This conversation will no longer show up in the current user's inbox
or archive and it will not be included in search results. If a new message is written in the
conversation, it will again show up in the user's inbox.

Get all Messages
-----------------

To get all messages for a given conversation, you must issue this request:

**GET /message/?conversation=[ID]**

Response:

You get a list of message resources for this conversation, this parameters:

    :created_date: The date and time that the conversation was created.
    :id: The id of the message.
    :message: The actual message (Text/String).
    :user: The user that sent the message. It's null if the user removed his/her account.
    :user_deleted_name: Is the name (just a string) of the user that sent the message in the first place, just as a reference.

Post a new Message
------------------

**POST /message/**

Arguments:

    You must provide the conversation_id and the message. Example:

    {"conversation_id": ID, "message": "Message from API!"}

Response Header:

    Location: https://athlete.com/api/v1/message/[ID]/

A note regarding deleted users and messages
-------------------------------------------

Sometimes users decide to remove their account from Athlete.com. If such user is involved in some conversation, we don't want to lose his/her messages, because the conversation could lost its sense. In those cases, we provide some mechanisms for the user browsing the conversation to note that. In the case of conversation, you have a list of names (past_users_involved) that indicate all the users that wer previously involved in the conversation but decided to remove their accounts.

For each message, if the user that sent the message removed his/her account, the "user" field will be null, but you'll see the name as an string in the "user_deleted_name" field.
