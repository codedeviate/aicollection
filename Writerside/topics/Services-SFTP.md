# SFTP

The Secure File Transfer Protocol (SFTP) is a network protocol that provides file access, file transfer, and file management functionalities over a reliable data stream. It is part of the SSH (Secure Shell) protocol suite and provides secure file transfer capabilities.

## Key Concepts of SFTP

- **Client-Server Model**: SFTP operates on a client-server model where the client initiates a connection to the server to transfer files.
- **Secure Connection**: SFTP uses SSH to encrypt both the command and data channels, ensuring secure file transfer.
- **Authentication**: SFTP requires authentication, typically using a username and password or SSH keys.
- **File Operations**: SFTP supports various file operations such as uploading, downloading, renaming, and deleting files.

## SFTP Commands

- **put**: Uploads a file to the server.
- **get**: Downloads a file from the server.
- **ls**: Lists files and directories on the server.
- **rm**: Deletes a file on the server.
- **rename**: Renames a file on the server.
- **mkdir**: Creates a directory on the server.
- **rmdir**: Removes a directory on the server.

## SFTP Status codes

SFTP (Secure File Transfer Protocol) does not use response codes in the same way that FTP does. Instead, SFTP uses status codes to indicate the result of an operation. Here are some common SFTP status codes:

- **0**: OK
- **1**: EOF (End of File)
- **2**: No such file
- **3**: Permission denied
- **4**: Failure
- **5**: Bad message
- **6**: No connection
- **7**: Connection lost
- **8**: Operation unsupported

These status codes are used to indicate the success or failure of various SFTP operations.

## Example: Uploading and Downloading Files Using Python's Paramiko

Here is an example of uploading and downloading files using Python's `paramiko` library:

```python
import paramiko

# SFTP server configuration
sftp_server = 'sftp.example.com'
sftp_port = 22
sftp_user = 'your_username'
sftp_password = 'your_password'

# Connect to the server
transport = paramiko.Transport((sftp_server, sftp_port))
transport.connect(username=sftp_user, password=sftp_password)

# Create an SFTP session
sftp = paramiko.SFTPClient.from_transport(transport)

# Upload a file
local_file = 'upload.txt'
remote_file = '/remote/path/upload.txt'
sftp.put(local_file, remote_file)

# Download a file
local_file = 'download.txt'
remote_file = '/remote/path/download.txt'
sftp.get(remote_file, local_file)

# List files in the remote directory
for filename in sftp.listdir('/remote/path'):
    print(filename)

# Close the connection
sftp.close()
transport.close()
```

## Relevant Switches and Parameters

### Common `paramiko.SFTPClient` Methods
- `put(localpath, remotepath)`: Uploads a file to the server.
- `get(remotepath, localpath)`: Downloads a file from the server.
- `listdir(path)`: Lists files and directories in the specified path.
- `remove(path)`: Deletes a file on the server.
- `rename(oldpath, newpath)`: Renames a file on the server.
- `mkdir(path)`: Creates a directory on the server.
- `rmdir(path)`: Removes a directory on the server.

Understanding SFTP and its associated commands and responses is crucial for implementing and troubleshooting secure file transfer services.