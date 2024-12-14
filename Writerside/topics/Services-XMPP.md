# XMPP

The Extensible Messaging and Presence Protocol (XMPP) is a communication protocol for message-oriented middleware based on XML (Extensible Markup Language). It enables the near-real-time exchange of structured data between any two or more network entities.

## Key Concepts of XMPP

- **Client-Server Model**: XMPP operates on a client-server model where clients connect to a server to exchange messages.
- **Decentralized Network**: XMPP is designed to be decentralized, meaning there is no central server, and any server can communicate with any other server.
- **Presence Information**: XMPP supports presence information, allowing users to see the availability status of their contacts.
- **Extensibility**: XMPP is highly extensible, allowing for the addition of new features and protocols through XMPP Extension Protocols (XEPs).

## XMPP Core Features

- **Messaging**: Sending and receiving messages between clients.
- **Presence**: Broadcasting and receiving presence information (e.g., online, offline, away).
- **Roster Management**: Managing a list of contacts (roster) and their presence information.
- **Subscription Management**: Subscribing to and unsubscribing from presence information of other users.

## XMPP Stanzas

XMPP (Extensible Messaging and Presence Protocol) does not use response codes in the same way that HTTP or FTP does. Instead, XMPP uses XML stanzas to communicate between clients and servers. These stanzas include:

- **Message**: Used for sending messages between clients.
- **Presence**: Used for broadcasting and receiving presence information.
- **IQ (Info/Query)**: Used for requesting and responding to information queries.

Each stanza can include error conditions, which are represented as XML elements within the stanza. Some common XMPP error conditions include:

- **bad-request**: The request is malformed or contains invalid data.
- **conflict**: There is a conflict, such as a resource conflict.
- **feature-not-implemented**: The requested feature is not implemented by the server.
- **forbidden**: The action is forbidden.
- **gone**: The recipient is no longer available.
- **internal-server-error**: The server encountered an internal error.
- **item-not-found**: The requested item was not found.
- **jid-malformed**: The provided JID (Jabber ID) is malformed.
- **not-acceptable**: The request is not acceptable.
- **not-allowed**: The action is not allowed.
- **not-authorized**: The sender is not authorized to perform the action.
- **policy-violation**: The action violates a policy.
- **recipient-unavailable**: The recipient is unavailable.
- **redirect**: The recipient has moved to a new address.
- **registration-required**: Registration is required to perform the action.
- **remote-server-not-found**: The remote server was not found.
- **remote-server-timeout**: The remote server did not respond in time.
- **resource-constraint**: The server is experiencing resource constraints.
- **service-unavailable**: The service is unavailable.
- **subscription-required**: A subscription is required to perform the action.
- **undefined-condition**: An undefined error condition occurred.
- **unexpected-request**: The request was unexpected.

## Example: Sending and Receiving Messages Using Python's `slixmpp` Library

Here is an example of sending and receiving messages using Python's `slixmpp` library:

```python
import slixmpp

class SendMsgBot(slixmpp.ClientXMPP):
    def __init__(self, jid, password, recipient, message):
        super().__init__(jid, password)
        self.recipient = recipient
        self.message = message
        self.add_event_handler("session_start", self.start)
        self.add_event_handler("message", self.message_received)

    def start(self, event):
        self.send_presence()
        self.get_roster()
        self.send_message(mto=self.recipient, mbody=self.message, mtype='chat')
        self.disconnect(wait=True)

    def message_received(self, msg):
        if msg['type'] in ('chat', 'normal'):
            print(f"Message received from {msg['from']}: {msg['body']}")

# XMPP server configuration
jid = 'your_username@example.com'
password = 'your_password'
recipient = 'recipient@example.com'
message = 'Hello, this is a test message.'

# Create and start the bot
xmpp = SendMsgBot(jid, password, recipient, message)
xmpp.connect()
xmpp.process(forever=False)
```

## Relevant Switches and Parameters

### Common `slixmpp.ClientXMPP` Methods
- `ClientXMPP(jid, password)`: Initializes the XMPP client with the given JID and password.
- `add_event_handler(event, handler)`: Adds an event handler for a specific event.
- `send_presence()`: Sends presence information to the server.
- `get_roster()`: Retrieves the roster (contact list) from the server.
- `send_message(mto, mbody, mtype)`: Sends a message to the specified recipient.
- `disconnect(wait)`: Disconnects from the server.

Understanding XMPP and its associated features and methods is crucial for implementing and troubleshooting real-time messaging services.