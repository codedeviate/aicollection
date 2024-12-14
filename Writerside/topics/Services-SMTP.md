# SMTP

The Simple Mail Transfer Protocol (SMTP) is a protocol used for sending emails across networks. It is a part of the application layer of the TCP/IP protocol suite and is used to transfer mail from a client to a server or between servers.

## Key Concepts of SMTP

- **Client-Server Model**: SMTP operates on a client-server model where the client sends an email to the server, which then forwards it to the recipient's server.
- **Commands and Responses**: SMTP uses a set of commands and responses to communicate between the client and server.
- **Ports**: SMTP typically uses port 25 for non-encrypted communication, port 587 for encrypted communication (STARTTLS), and port 465 for SMTPS (SMTP over SSL).

## SMTP Commands

- **HELO/EHLO**: Initiates the conversation between the client and server.
- **MAIL FROM**: Specifies the sender's email address.
- **RCPT TO**: Specifies the recipient's email address.
- **DATA**: Indicates the start of the message content.
- **RSET**: Resets the current mail transaction.
- **VRFY**: Verifies an email address.
- **EXPN**: Expands a mailing list.
- **HELP**: Provides help information.
- **NOOP**: No operation (keeps the connection alive).
- **QUIT**: Terminates the session.
- **STARTTLS**: Initiates TLS encryption.
- **AUTH**: Authenticates the client to the server.

## SMTP Responses

- **211**: System status, or system help reply
- **214**: Help message
- **220**: Service ready
- **221**: Service closing transmission channel
- **250**: Requested mail action okay, completed
- **251**: User not local; will forward to &lt;forward-path&gt;
- **252**: Cannot VRFY user, but will accept message and attempt delivery
- **354**: Start mail input; end with &lt;CRLF&gt;.&lt;CRLF&gt;
- **421**: Service not available, closing transmission channel
- **450**: Requested mail action not taken: mailbox unavailable
- **451**: Requested action aborted: local error in processing
- **452**: Requested action not taken: insufficient system storage
- **500**: Syntax error, command unrecognized
- **501**: Syntax error in parameters or arguments
- **502**: Command not implemented
- **503**: Bad sequence of commands
- **504**: Command parameter not implemented
- **550**: Requested action not taken: mailbox unavailable
- **551**: User not local; please try &lt;forward-path&gt;
- **552**: Requested mail action aborted: exceeded storage allocation
- **553**: Requested action not taken: mailbox name not allowed
- **554**: Transaction failed

## Example: Sending an Email Using Python's smtplib

Here is an example of sending an email using Python's `smtplib` library:

```python
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart

# SMTP server configuration
smtp_server = 'smtp.example.com'
smtp_port = 587
smtp_user = 'your_email@example.com'
smtp_password = 'your_password'

# Email content
sender_email = 'your_email@example.com'
receiver_email = 'receiver@example.com'
subject = 'Test Email'
body = 'This is a test email sent using Python.'

# Create the email message
msg = MIMEMultipart()
msg['From'] = sender_email
msg['To'] = receiver_email
msg['Subject'] = subject
msg.attach(MIMEText(body, 'plain'))

# Send the email
try:
    server = smtplib.SMTP(smtp_server, smtp_port)
    server.starttls()  # Secure the connection
    server.login(smtp_user, smtp_password)
    server.sendmail(sender_email, receiver_email, msg.as_string())
    print('Email sent successfully')
except Exception as e:
    print(f'Error: {e}')
finally:
    server.quit()
```

## Relevant Switches and Parameters

### Common `smtplib.SMTP` Methods
- `SMTP(server, port)`: Connects to the SMTP server.
- `starttls()`: Secures the SMTP connection using TLS.
- `login(user, password)`: Authenticates with the SMTP server.
- `sendmail(from_addr, to_addrs, msg)`: Sends an email.

Understanding SMTP and its associated commands and responses is crucial for implementing and troubleshooting email services.