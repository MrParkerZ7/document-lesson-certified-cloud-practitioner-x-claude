# 📦 AWS Container Services

## File Structure

```
lesson-11-aws-compute-services/
└── 02-container-services/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Container services on AWS allow you to run containerized applications without managing the underlying infrastructure. AWS provides managed services for container orchestration, making it easier to deploy, manage, and scale containerized workloads.

## Container Basics

```
+------------------------------------------------------------------+
|                    CONTAINERS vs VMs                              |
+------------------------------------------------------------------+
|                                                                   |
|   VIRTUAL MACHINES                   CONTAINERS                   |
|   +------------------+               +------------------+         |
|   | App A  | App B   |               | App A | App B | App C|     |
|   +--------+---------+               +-------+-------+------+     |
|   | Guest  | Guest   |               |   Container Runtime   |    |
|   | OS     | OS      |               +-----------------------+    |
|   +--------+---------+               |     Host OS           |    |
|   |    Hypervisor    |               +-----------------------+    |
|   +------------------+               |     Infrastructure    |    |
|   |    Host OS       |               +-----------------------+    |
|   +------------------+                                            |
|   |  Infrastructure  |               Containers share host OS    |
|   +------------------+               = Lightweight, fast startup  |
|                                                                   |
+------------------------------------------------------------------+
```

## Container Benefits

| Benefit | Description |
|---------|-------------|
| Portability | Run anywhere (dev, test, prod) |
| Consistency | Same environment everywhere |
| Lightweight | Share host OS kernel |
| Fast startup | Start in seconds |
| Efficiency | Higher density than VMs |
| Isolation | Process-level isolation |

## AWS Container Services Overview

| Service | Description | Management Level |
|---------|-------------|------------------|
| Amazon ECS | Container orchestration | AWS managed |
| Amazon EKS | Kubernetes on AWS | AWS managed |
| AWS Fargate | Serverless containers | Fully managed |
| Amazon ECR | Container registry | AWS managed |

## Amazon ECS (Elastic Container Service)

```
+------------------------------------------------------------------+
|                      AMAZON ECS                                   |
+------------------------------------------------------------------+
|                                                                   |
|   ECS = AWS-Native Container Orchestration                        |
|                                                                   |
|   +------------------+     +------------------+                   |
|   |    ECS Cluster   |     |    ECS Cluster   |                   |
|   |                  |     |                  |                   |
|   |  +-----------+   |     |  +-----------+   |                   |
|   |  | Service   |   |     |  | Service   |   |                   |
|   |  |           |   |     |  |           |   |                   |
|   |  | [Task]    |   |     |  | [Task]    |   |                   |
|   |  | [Task]    |   |     |  | [Task]    |   |                   |
|   |  +-----------+   |     |  +-----------+   |                   |
|   |                  |     |                  |                   |
|   |  Launch Type:    |     |  Launch Type:    |                   |
|   |  EC2 or Fargate  |     |  EC2 or Fargate  |                   |
|   +------------------+     +------------------+                   |
|                                                                   |
+------------------------------------------------------------------+
```

## ECS Components

| Component | Description |
|-----------|-------------|
| Cluster | Logical grouping of services and tasks |
| Task Definition | Blueprint for your container (image, CPU, memory) |
| Task | Running instance of a task definition |
| Service | Manages desired count of tasks |
| Container Instance | EC2 instance running ECS agent |

## ECS Launch Types

| Launch Type | Description | You Manage |
|-------------|-------------|------------|
| EC2 | Containers run on EC2 instances | EC2 instances, OS patching |
| Fargate | Serverless container execution | Nothing - fully managed |

## Amazon EKS (Elastic Kubernetes Service)

```
+------------------------------------------------------------------+
|                      AMAZON EKS                                   |
+------------------------------------------------------------------+
|                                                                   |
|   EKS = Managed Kubernetes on AWS                                 |
|                                                                   |
|   +------------------------------------------------------------+ |
|   |                    EKS Control Plane                        | |
|   |  (AWS Managed - API Server, etcd, Scheduler)                | |
|   +------------------------------------------------------------+ |
|                              |                                    |
|   +------------------------------------------------------------+ |
|   |                    Worker Nodes                             | |
|   |  +------------------+  +------------------+                  | |
|   |  | EC2 or Fargate   |  | EC2 or Fargate   |                  | |
|   |  | [Pod] [Pod]      |  | [Pod] [Pod]      |                  | |
|   |  +------------------+  +------------------+                  | |
|   +------------------------------------------------------------+ |
|                                                                   |
+------------------------------------------------------------------+
```

## EKS Features

| Feature | Description |
|---------|-------------|
| Managed control plane | AWS manages Kubernetes masters |
| Worker nodes | EC2 or Fargate for pods |
| Kubernetes compatible | Standard Kubernetes APIs |
| Integration | Works with AWS services |
| Scaling | Auto scaling for nodes and pods |

## ECS vs EKS

| Feature | ECS | EKS |
|---------|-----|-----|
| Orchestration | AWS-native | Kubernetes |
| Learning curve | Lower | Higher |
| Portability | AWS-specific | Multi-cloud |
| Best for | AWS-only deployments | Kubernetes expertise |
| Pricing | No control plane fee | Control plane fee |

## AWS Fargate

```
+------------------------------------------------------------------+
|                      AWS FARGATE                                  |
+------------------------------------------------------------------+
|                                                                   |
|   Serverless Compute for Containers                               |
|                                                                   |
|   Traditional (EC2 Launch)         Fargate (Serverless)           |
|   +----------------------+        +----------------------+        |
|   | You manage:          |        | AWS manages:         |        |
|   | - EC2 instances      |        | - Infrastructure     |        |
|   | - Scaling            |        | - Scaling            |        |
|   | - OS patching        |        | - Patching           |        |
|   | - Cluster capacity   |        | - Everything         |        |
|   +----------------------+        +----------------------+        |
|                                                                   |
|   Fargate = "Just run my containers"                              |
|                                                                   |
+------------------------------------------------------------------+
```

## Fargate Benefits

| Benefit | Description |
|---------|-------------|
| No servers | No EC2 instances to manage |
| Right-sized | Pay for exact resources used |
| Secure | Isolation by design |
| Scalable | Scale without managing infrastructure |
| Works with | Both ECS and EKS |

## Amazon ECR (Elastic Container Registry)

| Feature | Description |
|---------|-------------|
| Purpose | Store and manage Docker images |
| Security | Encryption at rest, IAM integration |
| Availability | Highly available and scalable |
| Integration | Works with ECS, EKS, Lambda |
| Scanning | Vulnerability scanning for images |

## Container Workflow

```
+------------------------------------------------------------------+
|                   CONTAINER WORKFLOW                              |
+------------------------------------------------------------------+
|                                                                   |
|   1. BUILD              2. STORE              3. RUN              |
|   +----------+         +----------+         +----------+          |
|   | Docker   |  Push   | Amazon   |  Pull   | ECS/EKS  |          |
|   | Image    | ------> | ECR      | ------> | Fargate  |          |
|   +----------+         +----------+         +----------+          |
|                                                                   |
|   Developer builds     Images stored        Containers run        |
|   container image      in registry          on AWS                |
|                                                                   |
+------------------------------------------------------------------+
```

## Pricing Comparison

| Service | Pricing Model |
|---------|---------------|
| ECS | Free (pay for underlying EC2/Fargate) |
| EKS | $0.10/hour per cluster + EC2/Fargate |
| Fargate | Pay for vCPU and memory per second |
| ECR | Pay for storage and data transfer |

## When to Use Each Service

| Use Case | Recommended Service |
|----------|---------------------|
| Simple container orchestration | ECS + Fargate |
| Kubernetes expertise/requirement | EKS |
| Hybrid/multi-cloud | EKS |
| New to containers | ECS + Fargate |
| Serverless containers | Fargate |
| Store container images | ECR |

## 🎯 Exam Tips

- **ECS** = AWS-native container orchestration, simpler to use
- **EKS** = Managed Kubernetes, for K8s expertise or multi-cloud
- **Fargate** = Serverless containers, no servers to manage
- **ECR** = Container registry, stores Docker images
- **Fargate works with both ECS and EKS**
- **ECS has no control plane fee**, EKS has a fee per cluster
- **Containers** are lightweight, share host OS, faster than VMs
- Choose **ECS for simplicity**, **EKS for Kubernetes portability**

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Container | Lightweight, standalone package with code and dependencies |
| Docker | Popular container runtime and image format |
| ECS | Elastic Container Service, AWS container orchestration |
| EKS | Elastic Kubernetes Service, managed Kubernetes |
| Fargate | Serverless compute engine for containers |
| ECR | Elastic Container Registry, Docker image storage |
| Pod | Kubernetes unit of deployment (one or more containers) |
| Task | ECS unit of deployment |

## 💡 Key Takeaways

1. Containers are lightweight alternatives to VMs, sharing host OS
2. ECS is AWS-native container orchestration, simple to use
3. EKS is managed Kubernetes for K8s expertise or multi-cloud needs
4. Fargate provides serverless container execution for ECS or EKS
5. ECR stores and manages Docker container images
6. Choose ECS for simplicity, EKS for Kubernetes portability
7. Fargate eliminates need to manage EC2 instances for containers

---

*Next: [03 - Serverless Computing](../03-serverless-computing/readme.md)*
