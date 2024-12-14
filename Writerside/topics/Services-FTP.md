# FTP

The File Transfer Protocol (FTP) is a standard network protocol used to transfer files between a client and a server over a TCP-based network, such as the Internet. FTP is built on a client-server model architecture and uses separate control and data connections between the client and the server.

## Key Concepts of FTP

- **Client-Server Model**: FTP operates on a client-server model where the client initiates a connection to the server to transfer files.
- **Control and Data Connections**: FTP uses two separate channels: a control connection for sending commands and receiving responses, and a data connection for transferring files.
- **Active and Passive Modes**: FTP can operate in active or passive mode. In active mode, the server initiates the data connection to the client. In passive mode, the client initiates both control and data connections.
- **Authentication**: FTP requires a username and password for authentication, although anonymous FTP allows users to connect without credentials.

## FTP Commands

- **USER**: Specifies the username for authentication.
- **PASS**: Specifies the password for authentication.
- **LIST**: Lists the files and directories in the current directory.
- **RETR**: Retrieves a file from the server.
- **STOR**: Stores a file on the server.
- **DELE**: Deletes a file on the server.
- **QUIT**: Ends the session.

## FTP Responses

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
    - **331**: Username okay, need password.
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

## Example: Uploading and Downloading Files Using Python's ftplib

Here is an example of uploading and downloading files using Python's `ftplib` library:

```python
import ftplib

# FTP server configuration
ftp_server = 'ftp.example.com'
ftp_user = 'your_username'
ftp_password = 'your_password'

# Connect to the server
ftp = ftplib.FTP(ftp_server)
ftp.login(user=ftp_user, passwd=ftp_password)

# Upload a file
filename = 'upload.txt'
with open(filename, 'rb') as file:
    ftp.storbinary(f'STOR {filename}', file)

# Download a file
filename = 'download.txt'
with open(filename, 'wb') as file:
    ftp.retrbinary(f'RETR {filename}', file.write)

# List files in the current directory
ftp.retrlines('LIST')

# Logout and close the connection
ftp.quit()
```

## Relevant Switches and Parameters

### Common `ftplib.FTP` Methods
- `FTP(server)`: Connects to the FTP server.
- `login(user, passwd)`: Authenticates with the FTP server.
- `storbinary(cmd, file)`: Uploads a file in binary mode.
- `retrbinary(cmd, callback)`: Downloads a file in binary mode.
- `retrlines(cmd)`: Retrieves a list of files and directories.
- `quit()`: Ends the session.

Understanding FTP and its associated commands and responses is crucial for implementing and troubleshooting file transfer services.