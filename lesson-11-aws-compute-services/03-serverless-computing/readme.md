# ⚡ Serverless Computing

## File Structure

```
lesson-11-aws-compute-services/
└── 03-serverless-computing/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Serverless computing allows you to build and run applications without thinking about servers. AWS manages the infrastructure, automatically scaling resources and handling server maintenance. You only pay for the compute time you consume.

## What is Serverless?

```
+------------------------------------------------------------------+
|                    SERVERLESS COMPUTING                           |
+------------------------------------------------------------------+
|                                                                   |
|   Traditional                        Serverless                   |
|   +----------------------+          +----------------------+      |
|   | You manage:          |          | You manage:          |      |
|   | - Servers            |          | - Code only          |      |
|   | - Operating systems  |          |                      |      |
|   | - Capacity planning  |          | AWS manages:         |      |
|   | - Scaling            |          | - Infrastructure     |      |
|   | - Availability       |          | - Scaling            |      |
|   | - Patching           |          | - High availability  |      |
|   +----------------------+          +----------------------+      |
|                                                                   |
|   Serverless = Focus on code, not infrastructure                  |
|                                                                   |
+------------------------------------------------------------------+
```

## Serverless Benefits

| Benefit | Description |
|---------|-------------|
| No server management | AWS handles infrastructure |
| Auto scaling | Scales automatically with demand |
| Pay per use | Only pay when code runs |
| High availability | Built-in fault tolerance |
| Faster time to market | Focus on business logic |

## AWS Lambda

```
+------------------------------------------------------------------+
|                        AWS LAMBDA                                 |
+------------------------------------------------------------------+
|                                                                   |
|   Lambda = Run code without provisioning servers                  |
|                                                                   |
|   Event Sources              Lambda Function           Output     |
|   +---------------+         +---------------+         +-------+   |
|   | API Gateway   | ------> |               | ------> | S3    |   |
|   | S3 Events     | ------> |  Your Code    | ------> | DynamoDB|  |
|   | CloudWatch    | ------> |               | ------> | SNS   |   |
|   | DynamoDB      | ------> | (Function)    | ------> | SQS   |   |
|   | SNS/SQS       | ------> |               | ------> | Other |   |
|   +---------------+         +---------------+         +-------+   |
|                                                                   |
|   Triggers Lambda          Runs your code           Takes action  |
|                                                                   |
+------------------------------------------------------------------+
```

## Lambda Key Features

| Feature | Description |
|---------|-------------|
| Languages | Python, Node.js, Java, Go, Ruby, .NET, custom runtime |
| Execution | Up to 15 minutes per invocation |
| Memory | 128 MB to 10 GB |
| Concurrency | 1000 concurrent executions (default) |
| Pricing | Pay per request + compute time |
| Triggers | Many AWS services can invoke Lambda |

## Lambda Pricing

| Component | Description |
|-----------|-------------|
| Requests | $0.20 per 1 million requests |
| Duration | Charged per 1ms of execution |
| Free tier | 1 million requests/month free |
| Memory | Price scales with memory allocation |

## Lambda Use Cases

| Use Case | Description |
|----------|-------------|
| Data processing | Process files uploaded to S3 |
| API backends | Handle API Gateway requests |
| Scheduled tasks | Cron-like scheduled execution |
| Stream processing | Process Kinesis/DynamoDB streams |
| IoT backends | Process IoT device data |

## Lambda Execution Model

```
+------------------------------------------------------------------+
|                   LAMBDA EXECUTION                                |
+------------------------------------------------------------------+
|                                                                   |
|   1. EVENT              2. EXECUTION            3. RESULT         |
|   +----------+         +-------------+         +----------+       |
|   | Trigger  | ------> | Cold Start  | ------> | Response |       |
|   | Event    |         | or          |         | or       |       |
|   |          |         | Warm Start  |         | Output   |       |
|   +----------+         +-------------+         +----------+       |
|                              |                                    |
|                              v                                    |
|                        Execution Time                             |
|                        (up to 15 min)                             |
|                                                                   |
|   Cold Start = New container initialized                          |
|   Warm Start = Reuse existing container (faster)                  |
|                                                                   |
+------------------------------------------------------------------+
```

## Other Serverless Services

| Service | Description |
|---------|-------------|
| API Gateway | Serverless REST/WebSocket APIs |
| Step Functions | Serverless workflow orchestration |
| EventBridge | Serverless event bus |
| S3 | Serverless object storage |
| DynamoDB | Serverless NoSQL database |
| SNS/SQS | Serverless messaging |

## API Gateway

| Feature | Description |
|---------|-------------|
| Purpose | Create, publish, and manage APIs |
| Types | REST API, HTTP API, WebSocket API |
| Integration | Lambda, HTTP endpoints, AWS services |
| Features | Authentication, throttling, caching |

## AWS Step Functions

| Feature | Description |
|---------|-------------|
| Purpose | Orchestrate multiple Lambda functions |
| Visual | Visual workflow designer |
| States | Tasks, choices, parallel, wait states |
| Use case | Complex multi-step workflows |

## Serverless Application Model (SAM)

| Feature | Description |
|---------|-------------|
| Purpose | Framework for building serverless apps |
| Templates | Simplified CloudFormation for serverless |
| CLI | Local testing and deployment |
| Integration | Works with Lambda, API Gateway, DynamoDB |

## Lambda vs EC2

| Feature | Lambda | EC2 |
|---------|--------|-----|
| Server management | None | You manage |
| Scaling | Automatic | Manual or Auto Scaling |
| Pricing | Per request/duration | Per hour/second |
| Runtime | Up to 15 minutes | Unlimited |
| Best for | Event-driven, short tasks | Long-running processes |

## Serverless Architecture Example

```
+------------------------------------------------------------------+
|               SERVERLESS WEB APPLICATION                          |
+------------------------------------------------------------------+
|                                                                   |
|   Users                                                           |
|     |                                                             |
|     v                                                             |
|   +---------------+                                               |
|   | CloudFront    | <-- Static content from S3                    |
|   +---------------+                                               |
|     |                                                             |
|     v                                                             |
|   +---------------+     +---------------+     +---------------+   |
|   | API Gateway   | --> |   Lambda      | --> |   DynamoDB    |   |
|   | (REST API)    |     |   (Backend)   |     |   (Database)  |   |
|   +---------------+     +---------------+     +---------------+   |
|                                                                   |
|   All components are serverless - no servers to manage!           |
|                                                                   |
+------------------------------------------------------------------+
```

## Lambda Limits

| Limit | Value |
|-------|-------|
| Memory | 128 MB - 10,240 MB |
| Timeout | Max 15 minutes |
| Deployment package | 50 MB (zipped), 250 MB (unzipped) |
| Concurrent executions | 1,000 (default, can increase) |
| Environment variables | 4 KB total |

## 🎯 Exam Tips

- **Lambda** = run code without servers, pay per request + duration
- **Max execution time** = 15 minutes (not suitable for long-running tasks)
- Lambda can be triggered by **many AWS services** (S3, API Gateway, DynamoDB, etc.)
- **Cold start** = initial latency when new container starts
- **API Gateway** = create serverless APIs that trigger Lambda
- **Step Functions** = orchestrate multiple Lambda functions
- Lambda pricing = **requests + compute time** (1ms billing)
- Lambda is **event-driven** - code runs in response to events
- **Serverless = you manage code, AWS manages everything else**

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Serverless | Computing where cloud provider manages infrastructure |
| Lambda | AWS serverless compute service |
| Cold Start | Initial latency when Lambda initializes |
| Warm Start | Faster execution when container is reused |
| Event Source | Service that triggers Lambda execution |
| Invocation | Single execution of a Lambda function |
| Concurrency | Number of simultaneous executions |

## 💡 Key Takeaways

1. Serverless means you focus on code, AWS manages infrastructure
2. Lambda runs code without provisioning servers
3. Lambda max execution time is 15 minutes
4. Pay only for requests and compute time used
5. Lambda is event-driven - triggered by other AWS services
6. API Gateway creates serverless APIs that invoke Lambda
7. Step Functions orchestrates complex multi-step workflows
8. Serverless architecture: CloudFront + API Gateway + Lambda + DynamoDB

---

*Next: [04 - Other Compute Services](../04-other-compute-services/readme.md)*
