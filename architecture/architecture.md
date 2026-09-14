# We Are Navodayan — System Architecture

## 1. Overview

We Are Navodayan follows a cloud-native microservices architecture.

Web and mobile applications communicate with backend services through an
API Gateway. Services use REST for synchronous communication and Kafka for
asynchronous event-driven communication.

The platform is deployed on AWS and provisioned using AWS CDK.

## 2. High-Level Architecture

```text
                    ┌──────────────┐
                    │    Users     │
                    └──────┬───────┘
                           │
              ┌────────────┴────────────┐
              ▼                         ▼
         React Web              React Native
              │                         │
              └────────────┬────────────┘
                           ▼
                    API Gateway / ALB
                           │
        ┌──────────────────┼──────────────────┐
        ▼                  ▼                  ▼
   Auth Service       User Service        JNV Service
        │                  │                  │
        ▼                  ▼                  ▼
  Alumni Service    Community Service   Opportunity Service
        │                  │                  │
        └──────────────────┼──────────────────┘
                           │
                           ▼
                        Kafka / MSK
                           │
             ┌─────────────┼─────────────┐
             ▼             ▼             ▼
       Notification     Search        Analytics
          Service       Service        Service

        ┌──────────────────────────────────────┐
        │              AWS Services            │
        │ PostgreSQL | Redis | S3 | Lambda     │
        │ SQS | SNS | CloudWatch | Secrets     │
        └──────────────────────────────────────┘