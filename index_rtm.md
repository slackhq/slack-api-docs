# Real Time Messaging (RTM) API

The Real Time Messaging API is a WebSocket-based API that allows you to
receive events from Slack in real time and send messages as user. It is the
basis for all Slack clients. It's also commonly used with the
[bot user integration](/bot-users) to create helper bots for your team.


## Basics

To begin a RTM session make an [authenticated](/docs/oauth) call to [the
rtm.start API method](/methods/rtm.start). This provides an initial set of
team metadata and a message server WebSocket URL. Once you have connected to
the message server it will provide a stream of events, including both messages
and updates to the current state of the team. This allows a client to easily
maintain a synchronized local copy of all team data and messages.

The Websocket URLs provided by `rtm.start` are single-use and are only valid
for 30 seconds, so make sure to connect quickly. If you connect successfully
the first event received will be a hello:

	{
		"type": "hello"
	}

This will be followed by any events that occured between the call to
`rtm.start` and the connection to the message server. If you're reconnecting
after a network problem this initial set of events may include a response
to the last message sent on a previous connection (with a `reply_to`) so a
client can confirm that message was received.

If there was a problem connecting an error will be returned, including a
descriptive error message:

	{
		"type": "error",
		"error": {
			"code": 1,
			"msg": "Socket URL has expired"
		}
	}

## Events

Almost everything that happens in Slack will result in an event being sent to
all connected clients. The simplest event is a message sent from a user:

	{
		"type": "message",
		"ts": "1358878749.000002",
		"user": "U023BECGF",
		"text": "Hello"
	}

Every event has a `type` property which describes the type of event. Our
servers currently send the following event types:

{EVENT_TYPES}

New event types will be added in the future, clients should be able to handle
unexpected event types.

## Sending messages

You can send a message to Slack by sending JSON over the websocket connection.

Every event should have a unique (for that connection) positive integer
ID. All replies to that message will include this ID allowing the client to
correlate responses with the messages sent; replies may be "out of order"
due to the asynchronous nature of the message servers.

Also, as with events sent from the server, each event sent by the client has a
string `type` specifying what the message does – chat messages are of type
`message`.

So to post the text "Hello world" to a channel, you can send this JSON:

	{
		"id": 1,
		"type": "message",
		"channel": "C024BE91L",
		"text": "Hello world"
	}

You can send a message to a private group or direct message channel in the
same way, but using a Group ID (`C024BE91L`) or DM channel ID (`D024BE91L`).

The RTM API only supports posting simple messages formatted using our
[default message formatting mode](/docs/formatting). It does not support
[attachments](/docs/attachments) or other message formatting modes. To post a
more complex message as a user clients can call the
[chat.postMessage Web API method](/methods/chat.postMessage) with `as_user`
set to true.

Once the JSON has been sent to the server visual clients should immediately
display the text in the channel, grayed out or otherwise marked to indicate
that it is "pending". At some point after that, usually a few milliseconds
later, the server will send a confirmation that the message was received:

	{
		"ok": true,
		"reply_to": 1,
		"ts": "1355517523.000005",
		"text": "Hello world"
	}

Replies to messages sent by clients will always contain two properties: a
boolean `ok` indicating whether they succeeeded and an integer `reply_to`
indicating which message they are in response to.

In the case of a reply to a chat message, if successful, the reply will
contain the canonical recorded timestamp of the message. All messages within
a single channel are guaranteed to have a unique timestamp which is ASCII
sortable. Given the precision of the timestamp, clients should treat these
timestamps as strings, not floats/doubles. Once a successful reply has been
returned, the message in the chat log should no longer be grayed out - it has
now been delivered.

Chat message replies also contain the message text, which may vary from the
sent message due to URL detection.

If there is an error processing an event the message server will reply with an
error. For example:

	{
		"ok": false,
		"reply_to": 1,
		"error": {
			"code: 2,
			"msg": "message text is missing"
		}
	}

## Typing indicators

Clients can send a typing indicator to indicate that the user is currently
writing a message to send to a channel:

	{
		"id": 1,
		"type": "typing",
		"channel": "C024BE91L"
	}

This can be sent on every key press in the chat input unless one has been
sent in the last three seconds. Unless there is an error the server will not
send a reply, but it will send a "user_typing" event to all team members in
the channel.

## Ping and Pong

Clients should try to quickly detect disconnections, even in idle periods, so
that users can easily tell the difference between being disconnected and
everyone being quiet. Not all web browsers support the WebSocket ping spec, so
the RTM protocol also supports ping/pong messages. When there is no other
activity clients should send a ping every few seconds. To send a ping, send
the following JSON:

	{
		"id": 1234, // ID, see "sending messages" above
		"type": "ping",
		…
	}

You can supply any number of extra "flat" arguments (that is: only scalar
values, no arrays or objects). These will be included in the pong message that
is sent back. For example, a client could include a local timestamp in the
ping message so it can calculate round-trip latency:

	{
		"id": 1234,
		"type": "ping",
		"time": 1403299273342
	}

This will be included in the reply from the server:

	{
		"reply_to": 1234,
		"type": "pong",
		"time": 1403299273342
	}

## Limits

The message server will disconnect any client that sends a message longer than
16 kilobytes. This includes all parts of the message, including JSON syntax,
not just the message text. Clients should limit messages sent to channels to
4000 characters, which will always be under 16k bytes even with a message
comprised solely of non-BMP Unicode characters at 4 bytes each. If the message
is longer a client should prompt to split the message into multiple messages,
create a snippet or create a post.

As with all Slack APIs, the RTM API is subject to
[rate limits](/docs/rate-limits). Clients should not
send more than one message per second sustained. If you do you may receive an
error message or be disconnected.

## What's a WebSocket?

[WebSockets](https://en.wikipedia.org/wiki/WebSocket) are a standard way to open a long-lived bi-directional communication channel with a server over TCP. It's the protocol used when connecting to our [RTM API](/rtm). Many [contributions from our community](/community) support the particulars of connecting to Slack via a WebSocket.
