# 📡 AWS IoT Services

## File Structure

```
lesson-16-other-aws-services/
└── 06-iot-services/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

The Internet of Things (IoT) connects physical devices to the cloud, enabling data collection, monitoring, and control at scale. AWS provides a comprehensive set of IoT services that help organizations connect, manage, and analyze data from billions of devices. For the AWS Cloud Practitioner exam, understanding the core IoT services and their use cases is essential.

## What is IoT?

```
+------------------------------------------------------------------+
|                    INTERNET OF THINGS (IoT)                       |
+------------------------------------------------------------------+
|                                                                   |
|   PHYSICAL WORLD                              DIGITAL WORLD       |
|                                                                   |
|   ┌─────────────────────────────┐    ┌─────────────────────────┐  |
|   │                             │    │                         │  |
|   │  [🌡️] Temperature Sensors   │    │     AWS Cloud           │  |
|   │  [📹] Cameras               │    │                         │  |
|   │  [🚗] Vehicles              │────▶  • Process Data        │  |
|   │  [🏭] Industrial Equipment  │    │  • Store & Analyze      │  |
|   │  [🏠] Smart Home Devices    │◀────  • Trigger Actions     │  |
|   │  [⚡] Energy Meters         │    │  • Machine Learning     │  |
|   │                             │    │                         │  |
|   └─────────────────────────────┘    └─────────────────────────┘  |
|                                                                   |
|   Billions of devices generating data and taking actions          |
|                                                                   |
+------------------------------------------------------------------+
```

## AWS IoT Services Overview

```
+------------------------------------------------------------------+
|                    AWS IoT SERVICES OVERVIEW                      |
+------------------------------------------------------------------+
|                                                                   |
|   DEVICE SOFTWARE              CONNECTIVITY              CLOUD    |
|   ┌──────────────┐           ┌──────────────┐     ┌────────────┐  |
|   │              │           │              │     │            │  |
|   │ AWS IoT      │           │ AWS IoT      │     │ Analytics  │  |
|   │ Greengrass   │  ──────▶  │ Core         │────▶│ Lambda     │  |
|   │ (Edge)       │           │ (Cloud)      │     │ S3         │  |
|   │              │           │              │     │ DynamoDB   │  |
|   └──────────────┘           └──────────────┘     └────────────┘  |
|                                                                   |
|   Edge Computing             Message Broker        AWS Services   |
|   Local Processing           Device Management     Integration    |
|   Offline Capability         Security & Auth                      |
|                                                                   |
+------------------------------------------------------------------+
```

## AWS IoT Core

AWS IoT Core is the foundational service for connecting IoT devices to AWS. It provides secure, bi-directional communication between devices and the AWS cloud.

```
+------------------------------------------------------------------+
|                        AWS IoT CORE                               |
+------------------------------------------------------------------+
|                                                                   |
|   IoT DEVICES                  IoT CORE              AWS SERVICES |
|                                                                   |
|   ┌─────────┐                ┌──────────────────┐   ┌───────────┐ |
|   │ Sensor  │                │                  │   │  Lambda   │ |
|   │  🌡️    │ ──────────────▶│   Message Broker │──▶│           │ |
|   └─────────┘    MQTT        │   ┌──────────┐   │   └───────────┘ |
|   ┌─────────┐                │   │  Rules   │   │   ┌───────────┐ |
|   │ Camera  │ ──────────────▶│   │  Engine  │   │──▶│    S3     │ |
|   │  📹    │    HTTPS        │   └──────────┘   │   │           │ |
|   └─────────┘                │   ┌──────────┐   │   └───────────┘ |
|   ┌─────────┐                │   │  Device  │   │   ┌───────────┐ |
|   │ Vehicle │ ──────────────▶│   │  Shadow  │   │──▶│ DynamoDB  │ |
|   │  🚗    │   WebSocket     │   └──────────┘   │   │           │ |
|   └─────────┘                │                  │   └───────────┘ |
|                              └──────────────────┘   ┌───────────┐ |
|                                                     │ Kinesis   │ |
|   Protocols: MQTT, HTTPS, WebSocket, LoRaWAN        │           │ |
|                                                     └───────────┘ |
|                                                                   |
+------------------------------------------------------------------+
```

### IoT Core Components

| Component | Description |
|-----------|-------------|
| **Message Broker** | Routes messages between devices and AWS services |
| **Rules Engine** | Processes and routes messages based on conditions |
| **Device Shadow** | Virtual representation of device state |
| **Device Registry** | Organizes devices and tracks metadata |
| **Security & Identity** | Authentication and authorization for devices |

### MQTT Protocol

MQTT (Message Queuing Telemetry Transport) is a lightweight messaging protocol designed for IoT devices with limited resources and unreliable networks.

```
+------------------------------------------------------------------+
|                    MQTT PUBLISH/SUBSCRIBE                         |
+------------------------------------------------------------------+
|                                                                   |
|   PUBLISHER                    BROKER                 SUBSCRIBER  |
|                                                                   |
|   ┌─────────┐                ┌─────────┐            ┌─────────┐   |
|   │ Sensor  │                │  IoT    │            │ Lambda  │   |
|   │         │ ─ Publish ──▶  │  Core   │ ─ Push ──▶ │         │   |
|   │  🌡️    │                │  Broker │            │         │   |
|   └─────────┘                └─────────┘            └─────────┘   |
|                                                                   |
|   Topic: sensors/temperature/room1                                |
|   Payload: {"temp": 72, "unit": "F"}                              |
|                                                                   |
|   Benefits:                                                       |
|   • Lightweight (low bandwidth)                                   |
|   • Bi-directional communication                                  |
|   • Quality of Service (QoS) levels                               |
|   • Retained messages                                             |
|                                                                   |
+------------------------------------------------------------------+
```

### Device Shadow

Device Shadow maintains the current state of a device, allowing applications to interact with devices even when they are offline.

```
+------------------------------------------------------------------+
|                        DEVICE SHADOW                              |
+------------------------------------------------------------------+
|                                                                   |
|   DEVICE                      SHADOW                  APPLICATION |
|                                                                   |
|   ┌─────────┐              ┌───────────────┐        ┌─────────┐   |
|   │         │              │ {             │        │         │   |
|   │ Light   │◀──sync──────▶│  "reported": {│◀──────▶│ Mobile  │   |
|   │ Bulb    │              │    "on": true │        │   App   │   |
|   │  💡     │              │  },           │        │         │   |
|   │         │              │  "desired": { │        │         │   |
|   │ (Online │              │    "on": false│        │(Always  │   |
|   │    or   │              │  }            │        │ Online) │   |
|   │ Offline)│              │ }             │        │         │   |
|   └─────────┘              └───────────────┘        └─────────┘   |
|                                                                   |
|   When device comes online, it syncs with shadow                  |
|   Shadow shows last known state when device offline               |
|                                                                   |
+------------------------------------------------------------------+
```

### Rules Engine

The Rules Engine evaluates incoming messages and triggers actions based on defined conditions.

```
+------------------------------------------------------------------+
|                      IoT RULES ENGINE                             |
+------------------------------------------------------------------+
|                                                                   |
|   INCOMING MESSAGE              RULE                  ACTION      |
|                                                                   |
|   ┌────────────────┐        ┌──────────────┐    ┌──────────────┐  |
|   │ Topic:         │        │              │    │              │  |
|   │ sensors/temp   │  ──▶   │ SELECT *     │──▶ │ Store in     │  |
|   │                │        │ FROM 'sensors│    │ DynamoDB     │  |
|   │ Payload:       │        │ /temp'       │    │              │  |
|   │ {"temp": 100}  │        │ WHERE temp   │    └──────────────┘  |
|   │                │        │ > 90         │    ┌──────────────┐  |
|   └────────────────┘        │              │──▶ │ Send to      │  |
|                             │              │    │ SNS Alert    │  |
|                             └──────────────┘    └──────────────┘  |
|                                                                   |
|   SQL-like syntax for filtering and routing messages              |
|                                                                   |
+------------------------------------------------------------------+
```

### IoT Core Features

| Feature | Description |
|---------|-------------|
| Device Gateway | Connect millions of devices securely |
| Protocol Support | MQTT, HTTPS, WebSocket, LoRaWAN |
| Authentication | X.509 certificates, custom authorizers |
| Authorization | IoT policies for fine-grained access |
| Encryption | TLS for data in transit |
| Scalability | Automatic scaling to billions of messages |

### IoT Core Use Cases

| Use Case | Description |
|----------|-------------|
| Smart Home | Connect and control home devices |
| Industrial IoT | Monitor manufacturing equipment |
| Fleet Management | Track vehicles and assets |
| Healthcare | Remote patient monitoring |
| Agriculture | Smart farming sensors |
| Energy | Smart grid and meters |

## AWS IoT Greengrass

AWS IoT Greengrass extends AWS capabilities to edge devices, enabling local compute, messaging, data caching, and ML inference.

```
+------------------------------------------------------------------+
|                     AWS IoT GREENGRASS                            |
+------------------------------------------------------------------+
|                                                                   |
|   EDGE LOCATION                              AWS CLOUD            |
|   ┌─────────────────────────────────┐      ┌────────────────────┐ |
|   │       GREENGRASS CORE           │      │                    │ |
|   │  ┌─────────────────────────┐    │      │   AWS IoT Core     │ |
|   │  │   Lambda Functions      │    │      │                    │ |
|   │  │   (Local Execution)     │    │      │   Lambda           │ |
|   │  └─────────────────────────┘    │      │                    │ |
|   │  ┌─────────────────────────┐    │      │   S3               │ |
|   │  │   ML Inference          │    │◀────▶│                    │ |
|   │  │   (Local Models)        │    │ Sync │   SageMaker        │ |
|   │  └─────────────────────────┘    │      │                    │ |
|   │  ┌─────────────────────────┐    │      │   CloudWatch       │ |
|   │  │   Local Messaging       │    │      │                    │ |
|   │  │   (Device to Device)    │    │      └────────────────────┘ |
|   │  └─────────────────────────┘    │                            |
|   │               ▲                 │                            |
|   │               │                 │                            |
|   │  ┌────┐  ┌────┐  ┌────┐       │                            |
|   │  │ 🌡️ │  │ 📹 │  │ ⚙️ │       │   Local devices connect    |
|   │  └────┘  └────┘  └────┘       │   to Greengrass Core       |
|   │  Local Devices                 │                            |
|   └─────────────────────────────────┘                            |
|                                                                   |
|   Works even when disconnected from the cloud!                    |
|                                                                   |
+------------------------------------------------------------------+
```

### IoT Greengrass Features

| Feature | Description |
|---------|-------------|
| Local Compute | Run Lambda functions at the edge |
| ML Inference | Deploy ML models for local predictions |
| Local Messaging | Device-to-device communication |
| Data Sync | Sync with cloud when connected |
| Offline Operation | Continue working without connectivity |
| Stream Manager | Manage data streams to cloud |
| Secret Manager | Securely access secrets at edge |
| Component Management | Deploy and manage edge applications |

### Greengrass vs IoT Core

| Feature | IoT Core | IoT Greengrass |
|---------|----------|----------------|
| **Location** | Cloud only | Edge + Cloud |
| **Processing** | In the cloud | At the edge (local) |
| **Connectivity** | Requires internet | Works offline |
| **Latency** | Internet dependent | Low (local) |
| **Use Case** | Cloud-centric IoT | Edge computing |
| **ML Inference** | Cloud-based | Local models |

### Greengrass Use Cases

| Use Case | Description |
|----------|-------------|
| Factory Automation | Local processing with cloud sync |
| Predictive Maintenance | ML inference at the edge |
| Video Analytics | Process video locally |
| Remote Locations | Operate with intermittent connectivity |
| Latency-Sensitive | Real-time local decisions |

```
+------------------------------------------------------------------+
|                 GREENGRASS ARCHITECTURE EXAMPLE                   |
+------------------------------------------------------------------+
|                                                                   |
|   SMART FACTORY                                                   |
|                                                                   |
|   ┌─────────────────────────────────────────────────────────────┐ |
|   │                  FACTORY FLOOR                               │ |
|   │                                                              │ |
|   │  ┌──────────────────────────────┐                           │ |
|   │  │     Greengrass Core          │                           │ |
|   │  │  ┌────────┐ ┌──────────────┐ │                           │ |
|   │  │  │ Lambda │ │ ML Model     │ │      ┌─────────────────┐  │ |
|   │  │  │ Filter │ │ (Anomaly     │ │──────│ AWS Cloud       │  │ |
|   │  │  │ Data   │ │  Detection)  │ │      │ (Periodic Sync) │  │ |
|   │  │  └────────┘ └──────────────┘ │      └─────────────────┘  │ |
|   │  └──────────────────────────────┘                           │ |
|   │           ▲         ▲         ▲                              │ |
|   │           │         │         │                              │ |
|   │      ┌────┴───┐ ┌───┴───┐ ┌───┴───┐                         │ |
|   │      │Machine │ │Machine│ │Machine│                         │ |
|   │      │   1    │ │   2   │ │   3   │                         │ |
|   │      └────────┘ └───────┘ └───────┘                         │ |
|   │                                                              │ |
|   │   • Real-time anomaly detection (local)                      │ |
|   │   • Aggregate data sent to cloud                             │ |
|   │   • Works during network outages                             │ |
|   │                                                              │ |
|   └─────────────────────────────────────────────────────────────┘ |
|                                                                   |
+------------------------------------------------------------------+
```

## Other AWS IoT Services

| Service | Description |
|---------|-------------|
| **IoT Device Defender** | Security monitoring and auditing for IoT devices |
| **IoT Device Management** | Onboard, organize, monitor, and manage devices |
| **IoT Analytics** | Analyze IoT data without managing infrastructure |
| **IoT Events** | Detect and respond to events from IoT sensors |
| **IoT SiteWise** | Collect and analyze industrial equipment data |
| **IoT FleetWise** | Collect vehicle data at scale |

## IoT Security

```
+------------------------------------------------------------------+
|                       IoT SECURITY                                |
+------------------------------------------------------------------+
|                                                                   |
|   DEVICE AUTHENTICATION          AUTHORIZATION                    |
|   ┌─────────────────────┐       ┌─────────────────────┐          |
|   │                     │       │                     │          |
|   │  X.509 Certificates │       │   IoT Policies      │          |
|   │  (Device Identity)  │       │   (Permissions)     │          |
|   │                     │       │                     │          |
|   │  • Unique per device│       │  • Topic access     │          |
|   │  • AWS CA signed    │       │  • Actions allowed  │          |
|   │  • Automatic renewal│       │  • Resource limits  │          |
|   │                     │       │                     │          |
|   └─────────────────────┘       └─────────────────────┘          |
|                                                                   |
|   ENCRYPTION                     MONITORING                       |
|   ┌─────────────────────┐       ┌─────────────────────┐          |
|   │                     │       │                     │          |
|   │  TLS 1.2+           │       │  IoT Device Defender│          |
|   │  (Data in Transit)  │       │  (Security Auditing)│          |
|   │                     │       │                     │          |
|   │  • Mutual TLS auth  │       │  • Audit policies   │          |
|   │  • Encrypted MQTT   │       │  • Detect anomalies │          |
|   │  • Certificate auth │       │  • Alert on issues  │          |
|   │                     │       │                     │          |
|   └─────────────────────┘       └─────────────────────┘          |
|                                                                   |
+------------------------------------------------------------------+
```

## IoT Architecture Patterns

| Pattern | Description | When to Use |
|---------|-------------|-------------|
| Cloud-Centric | All processing in AWS | Simple IoT, always connected |
| Edge Computing | Processing at the edge with Greengrass | Latency-sensitive, offline needed |
| Hybrid | Mix of edge and cloud | Balance of both requirements |

## IoT Service Selection Guide

| Requirement | Recommended Service |
|-------------|---------------------|
| Connect devices to cloud | AWS IoT Core |
| Run code at the edge | AWS IoT Greengrass |
| ML inference at edge | AWS IoT Greengrass |
| Security monitoring | AWS IoT Device Defender |
| Device fleet management | AWS IoT Device Management |
| Analyze IoT data | AWS IoT Analytics |
| Industrial data collection | AWS IoT SiteWise |

## 🎯 Exam Tips

- **IoT Core** = Connect devices to AWS cloud (message broker, rules engine)
- **IoT Greengrass** = Edge computing, local processing, offline operation
- **MQTT** = Lightweight protocol for IoT device communication
- **Device Shadow** = Virtual representation of device state (works offline)
- **Rules Engine** = SQL-like syntax to filter and route messages to AWS services
- IoT Core supports **billions of devices** and **trillions of messages**
- Greengrass enables **Lambda at the edge** and **ML inference** locally
- Greengrass works **offline** and syncs when connectivity restored
- IoT security uses **X.509 certificates** for device authentication
- **TLS encryption** for all device communication
- Remember: IoT Core = **cloud connectivity**, Greengrass = **edge computing**

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| IoT | Internet of Things - network of connected physical devices |
| Edge Computing | Processing data near the source rather than in the cloud |
| MQTT | Lightweight messaging protocol for IoT devices |
| Device Shadow | Cloud representation of device state |
| Message Broker | Routes messages between publishers and subscribers |
| Rules Engine | Processes messages and triggers actions |
| X.509 Certificate | Digital certificate for device identity |
| Telemetry | Automated collection and transmission of data |
| Sensor | Device that detects changes in the environment |
| Actuator | Device that takes physical action based on commands |

## 💡 Key Takeaways

1. AWS IoT Core connects devices to AWS with secure, bi-directional communication
2. IoT Core supports MQTT, HTTPS, and WebSocket protocols
3. Device Shadow maintains device state, enabling offline interaction
4. Rules Engine routes messages to AWS services using SQL-like syntax
5. AWS IoT Greengrass extends AWS to edge devices for local compute
6. Greengrass enables Lambda functions and ML inference at the edge
7. Greengrass continues operating when disconnected from the cloud
8. IoT devices authenticate using X.509 certificates
9. All IoT communication is encrypted with TLS
10. Choose IoT Core for cloud connectivity, Greengrass for edge computing
11. AWS IoT services scale to billions of devices and trillions of messages

---

[Previous: 05 - Frontend Web and Mobile](../05-frontend-web-and-mobile/readme.md) | [Next: Lesson 17 - AWS Pricing Models](../../lesson-17-aws-pricing-models/01-compute-purchasing-options/readme.md)
