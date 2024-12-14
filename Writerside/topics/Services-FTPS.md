# FTPS

FTPS (File Transfer Protocol Secure) is an extension to the commonly used File Transfer Protocol (FTP) that adds support for the Transport Layer Security (TLS) and the Secure Sockets Layer (SSL) cryptographic protocols. FTPS allows FTP to securely encrypt the control and data channels, ensuring the confidentiality and integrity of the data being transferred.

## Key Concepts of FTPS

- **Client-Server Model**: FTPS operates on a client-server model where the client initiates a connection to the server to transfer files.
- **Secure Connection**: FTPS uses TLS/SSL to encrypt both the command and data channels, ensuring secure file transfer.
- **Authentication**: FTPS requires authentication, typically using a username and password, and can also support client certificates.
- **Explicit and Implicit Modes**: FTPS can operate in explicit mode (where the client explicitly requests security from the server) or implicit mode (where the client connects to a secure port).

## FTPS Commands

FTPS uses the same commands as FTP, with the addition of commands to manage the secure connection:

- **USER**: Specifies the username for authentication.
- **PASS**: Specifies the password for authentication.
- **LIST**: Lists the files and directories in the current directory.
- **RETR**: Retrieves a file from the server.
- **STOR**: Stores a file on the server.
- **DELE**: Deletes a file on the server.
- **QUIT**: Ends the session.
- **AUTH**: Initiates a secure connection using TLS/SSL.
- **PBSZ**: Sets the size of the protection buffer.
- **PROT**: Sets the protection level for the data channel.

## FTPS Responses

FTPS uses the same response codes as FTP, with additional codes for secure connection management:

- **100 Series**: The requested action is being initiated, expect another reply before proceeding with a new command.
    - **110**: Restart marker reply.
    - **120**: Service ready in nnn minutes.
    - **125**: Data connection already open; transfer starting.
    - **150**: File status okay; about to open data connection.

- **200 Series**: The requested action has been successfully completed.
    - **200**: Command okay.
    - **202**: Command not implemented, superfluous at this site.
    - **211**: System status, or system help reply.
    - **212**: Directory status.
    - **213**: File status.
    - **214**: Help message.
    - **215**: NAME system type.
    - **220**: Service ready for new user.
    - **221**: Service closing control connection.
    - **225**: Data connection open; no transfer in progress.
    - **226**: Closing data connection. Requested file action successful.
    - **227**: Entering Passive Mode (h1,h2,h3,h4,p1,p2).
    - **230**: User logged in, proceed.
    - **250**: Requested file action okay, completed.
    - **257**: "PATHNAME" created.

- **300 Series**: The command has been accepted, but the requested action is on hold, pending receipt of further information.
    - **331**: User name okay, need password.
    - **332**: Need account for login.
    - **350**: Requested file action pending further information.

- **400 Series**: The command was not accepted and the requested action did not take place, but the error condition is temporary and the action may be requested again.
    - **421**: Service not available, closing control connection.
    - **425**: Can't open data connection.
    - **426**: Connection closed; transfer aborted.
    - **450**: Requested file action not taken.
    - **451**: Requested action aborted: local error in processing.
    - **452**: Requested action not taken. Insufficient storage space in system.

- **500 Series**: The command was not accepted and the requested action did not take place.
    - **500**: Syntax error, command unrecognized.
    - **501**: Syntax error in parameters or arguments.
    - **502**: Command not implemented.
    - **503**: Bad sequence of commands.
    - **504**: Command not implemented for that parameter.
    - **530**: Not logged in.
    - **532**: Need account for storing files.
    - **550**: Requested action not taken. File unavailable (e.g., file not found, no access).
    - **551**: Requested action aborted: page type unknown.
    - **552**: Requested file action aborted. Exceeded storage allocation.
    - **553**: Requested action not taken. File name not allowed.

- **FTPS Specific Codes**:
    - **234**: Indicates that the server accepts the AUTH command and is ready to negotiate a secure connection.
    - **334**: Indicates that the server is waiting for the client to send authentication information.
    - **631**: Indicates that the server has successfully negotiated a secure connection.

## Example: Uploading and Downloading Files Using Python's ftplib with TLS

Here is an example of uploading and downloading files using Python's `ftplib` library with TLS:

```python
import ftplib

# FTPS server configuration
ftps_server = 'ftps.example.com'
ftps_user = 'your_username'
ftps_password = 'your_password'

# Connect to the server
ftps = ftplib.FTP_TLS(ftps_server)
ftps.login(user=ftps_user, passwd=ftps_password)
ftps.prot_p()  # Secure the data connection

# Upload a file
filename = 'upload.txt'
with open(filename, 'rb') as file:
    ftps.storbinary(f'STOR {filename}', file)

# Download a file
filename = 'download.txt'
with open(filename, 'wb') as file:
    ftps.retrbinary(f'RETR {filename}', file.write)

# List files in the current directory
ftps.retrlines('LIST')

# Logout and close the connection
ftps.quit()
```

## Relevant Switches and Parameters

### Common `ftplib.FTP_TLS` Methods
- `FTP_TLS(server)`: Connects to the FTPS server.
- `login(user, passwd)`: Authenticates with the FTPS server.
- `prot_p()`: Secures the data connection using TLS.
- `storbinary(cmd, file)`: Uploads a file in binary mode.
- `retrbinary(cmd, callback)`: Downloads a file in binary mode.
- `retrlines(cmd)`: Retrieves a list of files and directories.
- `quit()`: Ends the session.

Understanding FTPS and its associated commands and responses is crucial for implementing and troubleshooting secure file transfer services.