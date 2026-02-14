# 🔗 AWS Application Integration Services

## File Structure

```
lesson-16-other-aws-services/
└── 01-application-integration/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS Application Integration services enable different applications, microservices, and distributed systems to communicate with each other. These services help decouple application components, making systems more resilient, scalable, and easier to maintain. Understanding these services is essential for the AWS Cloud Practitioner exam as they represent foundational building blocks for modern cloud architectures.

## Why Application Integration Matters

```
+------------------------------------------------------------------+
|           TIGHTLY COUPLED VS LOOSELY COUPLED ARCHITECTURE         |
+------------------------------------------------------------------+
|                                                                   |
|   TIGHTLY COUPLED (Traditional)     LOOSELY COUPLED (Modern)      |
|   ┌─────────────────────────┐      ┌─────────────────────────┐    |
|   │                         │      │                         │    |
|   │  [App A] ──▶ [App B]    │      │  [App A]                │    |
|   │     │                   │      │     │                   │    |
|   │     ▼                   │      │     ▼                   │    |
|   │  [App C] ──▶ [App D]    │      │  [Queue/Event Bus]      │    |
|   │                         │      │     │                   │    |
|   │  Problems:              │      │     ▼                   │    |
|   │  • One failure affects  │      │  [App B] [App C] [App D]│    |
|   │    entire system        │      │                         │    |
|   │  • Hard to scale        │      │  Benefits:              │    |
|   │  • Difficult to update  │      │  • Independent scaling  │    |
|   │                         │      │  • Fault isolation      │    |
|   └─────────────────────────┘      │  • Flexible updates     │    |
|                                    └─────────────────────────┘    |
|                                                                   |
+------------------------------------------------------------------+
```

## Amazon Simple Queue Service (SQS)

Amazon SQS is a fully managed message queuing service that enables you to decouple and scale microservices, distributed systems, and serverless applications.

```
+------------------------------------------------------------------+
|                        AMAZON SQS                                 |
+------------------------------------------------------------------+
|                                                                   |
|   PRODUCER                  QUEUE                   CONSUMER      |
|   ┌─────────┐           ┌─────────────┐          ┌─────────┐      |
|   │         │           │ ┌─┐┌─┐┌─┐┌─┐│          │         │      |
|   │  App A  │  ──▶      │ │1││2││3││4││   ──▶    │  App B  │      |
|   │         │  Send     │ └─┘└─┘└─┘└─┘│   Poll   │         │      |
|   └─────────┘           │   Messages  │          └─────────┘      |
|                         └─────────────┘                           |
|                                                                   |
|   Features:                                                       |
|   • Unlimited messages    • Auto-scaling                          |
|   • Message retention     • Dead-letter queues                    |
|   • Server-side encryption • Access policies                      |
|                                                                   |
+------------------------------------------------------------------+
```

### SQS Queue Types

| Queue Type | Description | Use Cases |
|------------|-------------|-----------|
| **Standard Queue** | Maximum throughput, at-least-once delivery, best-effort ordering | High throughput applications, decoupling components |
| **FIFO Queue** | First-In-First-Out delivery, exactly-once processing, limited to 300 TPS | Financial transactions, order processing |

### Key SQS Features

| Feature | Description |
|---------|-------------|
| Message Retention | Messages stored 1 minute to 14 days (default 4 days) |
| Message Size | Up to 256 KB per message |
| Visibility Timeout | Prevents other consumers from processing a message being processed |
| Dead-Letter Queue | Stores messages that fail processing after max retries |
| Long Polling | Reduces empty responses by waiting for messages |
| Encryption | Server-side encryption with AWS KMS |

## Amazon Simple Notification Service (SNS)

Amazon SNS is a fully managed pub/sub messaging service for application-to-application (A2A) and application-to-person (A2P) communication.

```
+------------------------------------------------------------------+
|                        AMAZON SNS                                 |
+------------------------------------------------------------------+
|                                                                   |
|   PUBLISHER               TOPIC                    SUBSCRIBERS    |
|   ┌─────────┐          ┌─────────┐              ┌─────────────┐   |
|   │         │          │         │   ──▶        │ Lambda      │   |
|   │  App    │  ──▶     │  SNS    │   ──▶        │ SQS Queue   │   |
|   │         │ Publish  │  Topic  │   ──▶        │ HTTP/HTTPS  │   |
|   └─────────┘          │         │   ──▶        │ Email       │   |
|                        └─────────┘   ──▶        │ SMS         │   |
|                                                 │ Mobile Push │   |
|                                                 └─────────────┘   |
|                                                                   |
|   Pattern: Publish-Subscribe (Fan-out)                            |
|   • One message to many recipients                                |
|   • Subscribers receive all messages published to topic           |
|                                                                   |
+------------------------------------------------------------------+
```

### SNS vs SQS Comparison

| Feature | SQS | SNS |
|---------|-----|-----|
| **Model** | Pull-based (polling) | Push-based (pub/sub) |
| **Delivery** | One consumer per message | Many subscribers |
| **Persistence** | Messages stored until consumed | No persistence |
| **Use Case** | Decouple apps, work queues | Notifications, fan-out |
| **Message Deletion** | Consumer deletes after processing | Auto-deleted after delivery |

### SNS Features

| Feature | Description |
|---------|-------------|
| Message Filtering | Subscribers receive only relevant messages based on filter policies |
| Message Fanout | Publish once, deliver to many subscribers |
| FIFO Topics | Ordered message delivery to FIFO SQS queues |
| Message Archiving | Archive messages to S3, Redshift, or other services |
| Encryption | Server-side encryption with AWS KMS |

## Amazon EventBridge

Amazon EventBridge is a serverless event bus that makes it easy to connect applications using events from your applications, SaaS apps, and AWS services.

```
+------------------------------------------------------------------+
|                      AMAZON EVENTBRIDGE                           |
+------------------------------------------------------------------+
|                                                                   |
|   EVENT SOURCES              EVENT BUS              TARGETS       |
|   ┌─────────────┐         ┌───────────┐         ┌─────────────┐   |
|   │ AWS Services│         │           │         │ Lambda      │   |
|   │ (EC2, S3)   │  ──▶    │  Default  │  ──▶    │ Step Func   │   |
|   └─────────────┘         │    Bus    │         │ SNS/SQS     │   |
|   ┌─────────────┐         │           │         │ Kinesis     │   |
|   │ Custom Apps │  ──▶    │  Custom   │  ──▶    │ API Gateway │   |
|   │             │         │    Bus    │         │ ECS Tasks   │   |
|   └─────────────┘         │           │         └─────────────┘   |
|   ┌─────────────┐         │  Partner  │                           |
|   │ SaaS Apps   │  ──▶    │    Bus    │              ▲            |
|   │ (Zendesk,   │         │           │              │            |
|   │  Datadog)   │         └───────────┘          RULES            |
|   └─────────────┘              │            (Filter & Route)      |
|                                ▼                                  |
|                         ┌───────────┐                             |
|                         │   Rules   │                             |
|                         │ (Pattern  │                             |
|                         │  Matching)│                             |
|                         └───────────┘                             |
|                                                                   |
+------------------------------------------------------------------+
```

### EventBridge Key Concepts

| Concept | Description |
|---------|-------------|
| Event Bus | Router that receives events and delivers to targets |
| Rules | Match incoming events and route to targets |
| Targets | AWS services that process events (Lambda, SQS, etc.) |
| Schema Registry | Store and discover event schemas |
| Archive & Replay | Archive events and replay them later |

### EventBridge vs SNS

| Feature | EventBridge | SNS |
|---------|-------------|-----|
| **Event Sources** | AWS, SaaS, Custom | Custom only |
| **Filtering** | Content-based rules | Attribute-based |
| **Schema** | Schema registry included | No schema support |
| **Pricing** | Pay per event | Pay per message |
| **Use Case** | Event-driven architectures | Simple pub/sub |

## AWS Step Functions

AWS Step Functions is a serverless orchestration service that lets you coordinate multiple AWS services into workflows called state machines.

```
+------------------------------------------------------------------+
|                      AWS STEP FUNCTIONS                           |
+------------------------------------------------------------------+
|                                                                   |
|   STATE MACHINE WORKFLOW:                                         |
|                                                                   |
|   ┌─────────┐     ┌─────────┐     ┌─────────┐     ┌─────────┐    |
|   │  Start  │ ──▶ │ Process │ ──▶ │  Choice │ ──▶ │ Success │    |
|   │         │     │  Order  │     │         │     │         │    |
|   └─────────┘     │(Lambda) │     └────┬────┘     └─────────┘    |
|                   └─────────┘          │                          |
|                                        │ Fail                     |
|                                        ▼                          |
|                                   ┌─────────┐     ┌─────────┐    |
|                                   │  Retry  │ ──▶ │  Fail   │    |
|                                   │         │     │         │    |
|                                   └─────────┘     └─────────┘    |
|                                                                   |
|   State Types:                                                    |
|   • Task - Do work (Lambda, ECS, etc.)                            |
|   • Choice - Branching logic                                      |
|   • Parallel - Run branches in parallel                           |
|   • Wait - Delay execution                                        |
|   • Pass - Pass input to output                                   |
|   • Succeed/Fail - Stop execution                                 |
|                                                                   |
+------------------------------------------------------------------+
```

### Step Functions Workflow Types

| Type | Description | Duration | Use Cases |
|------|-------------|----------|-----------|
| **Standard** | Exactly-once execution, durable | Up to 1 year | Long-running workflows |
| **Express** | At-least-once, high volume | Up to 5 minutes | High-event-rate processing |

### Step Functions Features

| Feature | Description |
|---------|-------------|
| Visual Workflow | Design and visualize workflows in AWS Console |
| Error Handling | Built-in retry and catch mechanisms |
| Service Integrations | 200+ AWS services directly integrated |
| Parallel Execution | Run multiple branches simultaneously |
| Human Approval | Pause workflow for human decisions |

## Amazon API Gateway

Amazon API Gateway is a fully managed service for creating, publishing, maintaining, monitoring, and securing APIs at any scale.

```
+------------------------------------------------------------------+
|                      AMAZON API GATEWAY                           |
+------------------------------------------------------------------+
|                                                                   |
|   CLIENTS              API GATEWAY              BACKENDS          |
|   ┌─────────┐         ┌───────────┐          ┌─────────────┐      |
|   │ Mobile  │         │           │          │ Lambda      │      |
|   │ Apps    │  ──▶    │  REST     │   ──▶    │             │      |
|   └─────────┘         │  API      │          └─────────────┘      |
|   ┌─────────┐         │           │          ┌─────────────┐      |
|   │ Web     │  ──▶    │  HTTP     │   ──▶    │ EC2         │      |
|   │ Apps    │         │  API      │          │             │      |
|   └─────────┘         │           │          └─────────────┘      |
|   ┌─────────┐         │ WebSocket │          ┌─────────────┐      |
|   │ IoT     │  ──▶    │  API      │   ──▶    │ Any HTTP    │      |
|   │ Devices │         │           │          │ Endpoint    │      |
|   └─────────┘         └───────────┘          └─────────────┘      |
|                             │                                     |
|                       ┌─────┴─────┐                               |
|                       │ Features: │                               |
|                       │• Auth     │                               |
|                       │• Throttle │                               |
|                       │• Cache    │                               |
|                       │• Monitor  │                               |
|                       └───────────┘                               |
|                                                                   |
+------------------------------------------------------------------+
```

### API Gateway API Types

| API Type | Description | Use Cases |
|----------|-------------|-----------|
| **REST API** | RESTful APIs with full features | Web/mobile backends |
| **HTTP API** | Lightweight, lower latency, lower cost | Simple APIs, proxies |
| **WebSocket API** | Two-way real-time communication | Chat apps, streaming |

### API Gateway Features

| Feature | Description |
|---------|-------------|
| Authentication | IAM, Cognito, Lambda authorizers, API keys |
| Throttling | Rate limiting and burst control |
| Caching | Response caching for improved performance |
| CORS | Cross-Origin Resource Sharing support |
| SDK Generation | Auto-generate client SDKs |
| Stages | Deploy to multiple environments (dev, prod) |
| Usage Plans | API keys with quotas and throttling |

## Application Integration Services Comparison

```
+------------------------------------------------------------------+
|              APPLICATION INTEGRATION SERVICES                     |
+------------------------------------------------------------------+
|                                                                   |
|   SERVICE          PATTERN              BEST FOR                  |
|   ┌──────────────────────────────────────────────────────────┐    |
|   │ SQS          Queue (Pull)         Decoupling, buffering  │    |
|   │ SNS          Pub/Sub (Push)       Fan-out, notifications │    |
|   │ EventBridge  Event Bus            Event-driven apps      │    |
|   │ Step Func    Orchestration        Complex workflows      │    |
|   │ API Gateway  Request/Response     API management         │    |
|   └──────────────────────────────────────────────────────────┘    |
|                                                                   |
|   COMMON PATTERNS:                                                |
|                                                                   |
|   SNS + SQS "Fanout"        API Gateway + Lambda "Serverless"     |
|   ┌─────┐                   ┌─────┐                               |
|   │ SNS │──▶ SQS Queue A    │ API │──▶ Lambda ──▶ DynamoDB        |
|   │Topic│──▶ SQS Queue B    │ GW  │                               |
|   └─────┘──▶ SQS Queue C    └─────┘                               |
|                                                                   |
+------------------------------------------------------------------+
```

## Service Selection Guide

| Requirement | Recommended Service |
|-------------|---------------------|
| Decouple services with message queue | Amazon SQS |
| Send notifications to multiple subscribers | Amazon SNS |
| React to events from AWS and SaaS apps | Amazon EventBridge |
| Orchestrate multiple AWS services | AWS Step Functions |
| Create and manage APIs | Amazon API Gateway |
| Real-time communication | API Gateway WebSocket |
| Fan-out messages to multiple queues | SNS + SQS |

## 🎯 Exam Tips

- **SQS** = Message queue for decoupling applications (pull-based, consumer polls for messages)
- **SNS** = Pub/sub messaging for notifications (push-based, delivers to subscribers)
- **SQS Standard** = Unlimited throughput, at-least-once delivery; **FIFO** = Ordered, exactly-once
- **SNS + SQS** together = Common pattern for fan-out to multiple queues
- **EventBridge** = Event bus for event-driven architectures, integrates with SaaS apps
- **Step Functions** = Orchestrate serverless workflows with visual state machines
- **API Gateway** = Create, manage, and secure APIs at any scale
- **API Gateway + Lambda** = Serverless backend pattern
- All these services are **fully managed** - no servers to manage
- Remember: SQS **decouples**, SNS **notifies**, EventBridge **routes events**, Step Functions **orchestrates**

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Message Queue | A buffer that stores messages between sender and receiver |
| Pub/Sub | Publishing messages to topics that subscribers receive |
| Event Bus | Central hub that routes events based on rules |
| Dead-Letter Queue | Queue that stores messages that fail processing |
| State Machine | Workflow defined as a series of states and transitions |
| Fanout | Pattern where one message is delivered to multiple recipients |
| Polling | Consumer requests messages from a queue |
| Push | Messages automatically delivered to subscribers |
| Decoupling | Separating application components for independent operation |
| Orchestration | Coordinating multiple services in a defined workflow |

## 💡 Key Takeaways

1. Amazon SQS is a message queue for decoupling applications using a pull-based model
2. Amazon SNS is a pub/sub service for sending notifications to multiple subscribers
3. SQS Standard offers unlimited throughput; FIFO guarantees order and exactly-once processing
4. SNS + SQS fanout is a common pattern for delivering messages to multiple queues
5. Amazon EventBridge is a serverless event bus for event-driven architectures
6. EventBridge integrates with AWS services, custom apps, and SaaS applications
7. AWS Step Functions orchestrates serverless workflows using visual state machines
8. Amazon API Gateway creates, publishes, and secures APIs at scale
9. API Gateway supports REST, HTTP, and WebSocket API types
10. These services are all fully managed with no servers to provision
11. Choose based on pattern: queue (SQS), pub/sub (SNS), events (EventBridge), orchestration (Step Functions)

---

[Previous: 02 - Analytics Services](../../lesson-15-aws-ai-ml-and-analytics-services/02-analytics-services/readme.md) | [Next: 02 - Business Applications](../02-business-applications/readme.md)
