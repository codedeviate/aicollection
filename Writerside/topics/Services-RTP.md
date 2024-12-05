# RTP

The Real-time Transport Protocol (RTP) is a network protocol for delivering audio and video over IP networks. It is widely used in communication and entertainment systems that involve streaming media, such as telephony, video teleconference applications, and web-based push-to-talk features.

## Key Concepts of RTP

- **Payload Type**: Identifies the format of the RTP payload and determines its interpretation by the application.
- **Sequence Number**: Used to detect packet loss and to restore packet sequence.
- **Timestamp**: Used to synchronize and play back media streams.
- **SSRC (Synchronization Source Identifier)**: Identifies the source of a stream. Each stream in a session has a unique SSRC.

## RTP Core Features

- **Real-time Transmission**: Designed for real-time data transmission, such as audio and video.
- **Synchronization**: Provides mechanisms for synchronizing different media streams.
- **Scalability**: Can be used in both unicast and multicast network configurations.
- **Extensibility**: Can be extended with additional features through RTP profiles and payload formats.

## Example: Sending and Receiving RTP Packets Using Python's `pylibsrtp` Library

Here is an example of sending and receiving RTP packets using Python's `pylibsrtp` library:

### Sender

```python
import socket
import time
import struct

# RTP packet parameters
RTP_VERSION = 2
PAYLOAD_TYPE = 96
SSRC = 12345
SEQUENCE_NUMBER = 0
TIMESTAMP = 0

# Create a UDP socket
sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
server_address = ('localhost', 5005)

def create_rtp_packet(payload):
    global SEQUENCE_NUMBER, TIMESTAMP
    header = struct.pack('!BBHII', (RTP_VERSION << 6) | (0 << 5) | PAYLOAD_TYPE, 0, SEQUENCE_NUMBER, TIMESTAMP, SSRC)
    SEQUENCE_NUMBER += 1
    TIMESTAMP += 160  # Assuming 20ms of audio at 8kHz
    return header + payload

# Send RTP packets
for i in range(10):
    payload = b'Hello RTP'
    packet = create_rtp_packet(payload)
    sock.sendto(packet, server_address)
    time.sleep(0.02)  # 20ms interval

sock.close()
```

### Receiver

```python
import socket
import struct

# Create a UDP socket
sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
server_address = ('localhost', 5005)
sock.bind(server_address)

def parse_rtp_packet(packet):
    header = packet[:12]
    payload = packet[12:]
    version, p, x, cc, m, pt, sequence_number, timestamp, ssrc = struct.unpack('!BBHII', header)
    return {
        'version': version >> 6,
        'payload_type': pt,
        'sequence_number': sequence_number,
        'timestamp': timestamp,
        'ssrc': ssrc,
        'payload': payload
    }

# Receive RTP packets
for i in range(10):
    packet, _ = sock.recvfrom(2048)
    rtp_packet = parse_rtp_packet(packet)
    print(f"Received RTP packet: {rtp_packet}")

sock.close()
```

## Relevant Switches and Parameters

### Common RTP Packet Fields
- **Version**: The version of RTP, typically set to 2.
- **Payload Type (PT)**: Indicates the format of the RTP payload.
- **Sequence Number**: Increments by one for each RTP packet sent.
- **Timestamp**: Reflects the sampling instant of the first byte in the RTP data packet.
- **SSRC**: Identifies the source of the RTP stream.

Understanding RTP and its associated features and methods is crucial for implementing and troubleshooting real-time media streaming services.