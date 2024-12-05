# SIP

The Session Initiation Protocol (SIP) is a signaling protocol used for initiating, maintaining, and terminating real-time sessions that include voice, video, and messaging applications. SIP is widely used in Internet telephony for voice and video calls, as well as in private IP telephone systems.

## Key Concepts of SIP

- **User Agents (UA)**: The endpoints in a SIP network, which can be clients (UAC) or servers (UAS).
- **Registrar**: A server that accepts REGISTER requests and updates the location database with the contact information of the user.
- **Proxy Server**: An intermediary entity that routes SIP requests to the user agent server.
- **Redirect Server**: A server that provides the client with information about the next hop or hops that a message should take.
- **Session Description Protocol (SDP)**: A protocol used to describe multimedia communication sessions for the purposes of session announcement, session invitation, and other forms of multimedia session initiation.

## SIP Methods

- **INVITE**: Initiates a call by inviting the user to participate in a session.
- **ACK**: Confirms that the client has received a final response to an INVITE request.
- **BYE**: Terminates a session between two users.
- **CANCEL**: Cancels any pending request.
- **REGISTER**: Registers the user agent with a SIP server.
- **OPTIONS**: Queries the capabilities of servers.
- **INFO**: Sends mid-session information that does not modify the session state.

## SIP Responses

- **1xx (Provisional)**: Informational responses, such as 100 Trying, 180 Ringing.
- **2xx (Success)**: Indicates that the request was successfully received, understood, and accepted, such as 200 OK.
- **3xx (Redirection)**: Further action needs to be taken to complete the request, such as 302 Moved Temporarily.
- **4xx (Client Error)**: The request contains bad syntax or cannot be fulfilled, such as 404 Not Found, 486 Busy Here.
- **5xx (Server Error)**: The server failed to fulfill a valid request, such as 500 Internal Server Error.
- **6xx (Global Failure)**: The request cannot be fulfilled at any server, such as 600 Busy Everywhere.

## Example: Implementing a Basic SIP Client Using `pjsip` Library

Here is an example of implementing a basic SIP client using the `pjsip` library in Python:

```python
import pjsua as pj

# Callback to receive events from the library
class MyAccountCallback(pj.AccountCallback):
    def __init__(self, account):
        pj.AccountCallback.__init__(self, account)

    def on_reg_state(self):
        print("Registration status: ", self.account.info().reg_status)

# Create a library instance
lib = pj.Lib()

try:
    # Initialize the library
    lib.init(log_cfg=pj.LogConfig(level=3))

    # Create a UDP transport which listens to any available port
    transport = lib.create_transport(pj.TransportType.UDP, pj.TransportConfig(5060))

    # Start the library
    lib.start()

    # Create an account
    acc_cfg = pj.AccountConfig("sip.example.com", "username", "password")
    acc_cb = MyAccountCallback(acc_cfg)
    acc = lib.create_account(acc_cfg, cb=acc_cb)

    # Wait for user input to end the program
    input("Press <ENTER> to quit\n")

    # Shutdown the library
    lib.destroy()
    lib = None

except pj.Error as e:
    print("Exception: " + str(e))
    lib.destroy()
    lib = None
```

## Relevant Switches and Parameters

### Common `pjsua` Methods
- `Lib()`: Initializes a new library instance.
- `init(log_cfg)`: Initializes the library with optional logging configuration.
- `create_transport(type, config)`: Creates a transport of the specified type (e.g., UDP).
- `start()`: Starts the library.
- `AccountConfig(domain, username, password)`: Configures an account with the specified domain, username, and password.
- `create_account(config, cb)`: Creates an account with the specified configuration and callback.
- `destroy()`: Shuts down the library and releases resources.

Understanding SIP and its associated methods and responses is crucial for implementing and troubleshooting real-time communication services.