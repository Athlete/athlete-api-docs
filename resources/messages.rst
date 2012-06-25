Conversations
==============

A user might be involved in a conversation. You can only fetch the conversations that your user is involved in.

Get Conversations
------------------

**GET /conversation/**

Arguments - None

Returns all the conversations, sorted by last active.

Get One Conversation
---------------------

**GET /conversation/[id]/**

You get some important fields:
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
