---
title: Monolith vs Microservice
updated: 2026-07-02T15:21:16+07:00
tags:
  - system-design
---

## Monolithic system


- All units (ex. UI,  Business Logic, Data Access Layer) are implemented in a **single components or codebase** and connect to **one database**.
- **Easy to deploy, debug, and maintain** because there's only one artifact to deploy. No complexities of coordinating deployments. Fewer resources are needed for infrastructure and monitoring
- This system can **scale [[system-scalability|vertically]] only**
- Suit to **small teams** and **create rapid prototype**
- Failure in one part **can impact the entire system**

## Microservice application

- One system **divided into small units**, communicating over a network
- Each service connect its own database
- **Multiple deployment processes**. Each service is deployed independently. Coordinating is needed.
- Due to the system is decentralized. If system need to be scale. it **can scale [[system-scalability|horizontally]]**
- Each service can be **develop in parallel** by **multiple teams**, using difference tech stack
- **More resources are needed** for infrastructure and monitoring (network, auth, logging, tracing)
- Need **large teams** to develop and maintain
- **Fault isolation**; Failure in one service don't affect others

## Resource

- https://www.geeksforgeeks.org/system-design/choosing-between-monolith-and-microservices-system-design-interview-hack/
- https://thenewstack.io/microservices/microservices-vs-monoliths-an-operational-comparison/
- https://medium.com/startlovingyourself/microservices-vs-monolithic-architecture-c8df91f16bb4
