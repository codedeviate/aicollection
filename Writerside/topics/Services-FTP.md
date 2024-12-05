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

- **200**: Command okay.
- **220**: Service ready for new user.
- **331**: User name okay, need password.
- **230**: User logged in, proceed.
- **550**: Requested action not taken (e.g., file not found, no access).

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