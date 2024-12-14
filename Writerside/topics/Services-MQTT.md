# MQTT

The Message Queuing Telemetry Transport (MQTT) is a lightweight, publish-subscribe network protocol that transports messages between devices. It is designed for connections with remote locations where a small code footprint is required or network bandwidth is limited. MQTT is widely used in IoT (Internet of Things) applications.

## Key Concepts of MQTT

- **Broker**: The server that receives all messages from the clients and then routes the messages to the appropriate destination clients.
- **Client**: Any device (from a microcontroller to a server) that runs an MQTT library and connects to an MQTT broker over a network.
- **Publish/Subscribe**: Clients can publish messages to a topic or subscribe to a topic to receive messages.
- **Topics**: Hierarchical strings that clients publish messages to and subscribe to.
- **Quality of Service (QoS)**: Defines the guarantee of delivery for a message. There are three levels:
    - **QoS 0**: At most once delivery.
    - **QoS 1**: At least once delivery.
    - **QoS 2**: Exactly once delivery.

## MQTT Core Features

- **Lightweight**: Minimal overhead, making it suitable for low-bandwidth and high-latency networks.
- **Scalable**: Can handle a large number of devices.
- **Reliable**: Provides different levels of Quality of Service (QoS) to ensure message delivery.

## MQTT Topics

In MQTT, topics are hierarchical strings that clients publish messages to and subscribe to. Topics are used to route messages between clients. Here are some key points about MQTT topics:

- **Hierarchical Structure**: Topics are structured in a hierarchy, with levels separated by slashes (`/`). For example, `home/livingroom/temperature`.
- **Wildcards**: MQTT supports two types of wildcards for subscribing to multiple topics:
  - **Single-level wildcard (`+`)**: Matches one level in the topic hierarchy. For example, `home/+/temperature` matches `home/livingroom/temperature` and `home/kitchen/temperature`.
  - **Multi-level wildcard (`#`)**: Matches any number of levels in the topic hierarchy. It must be the last character in the topic. For example, `home/#` matches `home/livingroom/temperature` and `home/kitchen/humidity`.

Here are some example MQTT topics:

- `home/livingroom/temperature`
- `home/kitchen/humidity`
- `sensors/+/status`
- `devices/#`

These topics allow for flexible and organized message routing in MQTT-based systems.

## MQTT Control Packets

Here are the MQTT commands, also known as control packets:

- **CONNECT**: Client request to connect to the server.
- **CONNACK**: Connect acknowledgment.
- **PUBLISH**: Publish message.
- **PUBACK**: Publish acknowledgment (QoS 1).
- **PUBREC**: Publish received (QoS 2, part 1).
- **PUBREL**: Publish release (QoS 2, part 2).
- **PUBCOMP**: Publish complete (QoS 2, part 3).
- **SUBSCRIBE**: Client subscribe request.
- **SUBACK**: Subscribe acknowledgment.
- **UNSUBSCRIBE**: Unsubscribe request.
- **UNSUBACK**: Unsubscribe acknowledgment.
- **PINGREQ**: PING request.
- **PINGRESP**: PING response.
- **DISCONNECT**: Client is disconnecting.
- **AUTH**: Authentication exchange.

## MQTT Acknowledgement Packets

MQTT does not use response codes in the same way that HTTP or FTP does. Instead, MQTT uses acknowledgment packets to indicate the status of message delivery and connection. Here are the key MQTT acknowledgment packets:

- **CONNACK**: Connection acknowledgment.
  - **0**: Connection accepted.
  - **1**: Connection refused, unacceptable protocol version.
  - **2**: Connection refused, identifier rejected.
  - **3**: Connection refused, server unavailable.
  - **4**: Connection refused, bad username or password.
  - **5**: Connection refused, not authorized.

- **PUBACK**: Publish acknowledgment for QoS 1 messages.
- **PUBREC**: Publish received (part of QoS 2 flow).
- **PUBREL**: Publish release (part of QoS 2 flow).
- **PUBCOMP**: Publish complete (part of QoS 2 flow).
- **SUBACK**: Subscribe acknowledgment.
- **UNSUBACK**: Unsubscribe acknowledgment.
- **PINGRESP**: Ping response.

These packets are used to manage the state and ensure the reliability of message delivery in MQTT.

## Example: Publishing and Subscribing Using Python's `paho-mqtt` Library

Here is an example of publishing and subscribing to MQTT topics using Python's `paho-mqtt` library:

### Publisher

```python
import paho.mqtt.client as mqtt

# MQTT broker configuration
broker = 'mqtt.example.com'
port = 1883
topic = 'test/topic'
message = 'Hello, MQTT!'

# Create a new MQTT client instance
client = mqtt.Client()

# Connect to the broker
client.connect(broker, port)

# Publish a message to the topic
client.publish(topic, message)

# Disconnect from the broker
client.disconnect()
```

### Subscriber

```python
import paho.mqtt.client as mqtt

# MQTT broker configuration
broker = 'mqtt.example.com'
port = 1883
topic = 'test/topic'

# Define the callback function for when a message is received
def on_message(client, userdata, msg):
    print(f"Received message: {msg.payload.decode()} on topic {msg.topic}")

# Create a new MQTT client instance
client = mqtt.Client()

# Set the on_message callback function
client.on_message = on_message

# Connect to the broker
client.connect(broker, port)

# Subscribe to the topic
client.subscribe(topic)

# Start the loop to process received messages
client.loop_forever()
```

## Relevant Switches and Parameters

### Common `paho.mqtt.client.Client` Methods
- `Client()`: Initializes a new MQTT client instance.
- `connect(host, port, keepalive)`: Connects to the MQTT broker.
- `disconnect()`: Disconnects from the MQTT broker.
- `publish(topic, payload, qos=0, retain=False)`: Publishes a message to a topic.
- `subscribe(topic, qos=0)`: Subscribes to a topic.
- `loop_forever()`: Starts a blocking loop to process network traffic and dispatch callbacks.
- `on_message`: Callback function that is called when a message is received.

Understanding MQTT and its associated features and methods is crucial for implementing and troubleshooting IoT applications and other real-time messaging services.