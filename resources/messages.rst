Conversations
==============

A user might be involved in a conversation. You can only fetch the conversations that your user is involved in. You might want to display information to your user informing the status of the conversations (read/unread). It's important to mark the conversation as read when you your user reads it.

Get Conversations
------------------

**GET /conversation/**

Arguments - None

Returns all the conversations for the logged in user. You can see it as the "Inbox" for that user. The first conversations will be the ones with unread messages. After that it's ordered just by date.

Get One Conversation
---------------------

**GET /conversation/[id]/**

You get some important fields:
    :has_unread_messages: shows if the currently logged in user have read all messages (true, false).
    :last_message: The last message from this conversation.
    :created_date: Date created this conversation.
    :recipients: A list of users, with all their information.
    :started_by: The user that started the conversation.

Mark conversations as read
---------------------------

We don't mark conversation as read when you fetch the messages for that particular conversation. This is really important. You have to explicitly inform us when the user has read the conversation. To do so, you must issue this request:

**PATCH /conversation/[ID]/read/**

Arguments

    :ID: is the ID of the conversation you want to mark as read
    :last_message_read_timestamp: A timestamp informing the timestamp of the last message read.

The "last_message_read_timestamp" must be provided becouse in the midtime between you fetch the messages and the time you issued this request, new messages might be created. The response for this method is:

    :200 Ok: if there are no new messages since the time you informed. You can safetly inform your user that he/she has read the conversation.
    :409 CONFLICT: New messages have been created. At this point you can fetch the messages again and reissue this request.

You can also use this method to know if there are new messages to display to your user.

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

Get all Messages
-----------------

To get all messages for a given conversation, you must issue this request:

**GET /message/?conversation=[ID]**

Response:

You get a list of message resources for this conversation, this parameters:

    :created_date: The date and time that the conversation was created.
    :id: The id of the message.
    :message: The actual message (Text/String).
    :user: The user that sent the message.

Post a new Message
------------------

**POST /message/**

Arguments:

    You must provide the conversation_id and the message. Example:

    {"conversation_id": ID, "message": "Message from API!"}

Response Header:

    Location: https://athlete.com/api/v1/message/[ID]/
