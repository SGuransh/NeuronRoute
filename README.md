# NeuronRoute: Distributed Machine Learning Inference Platform

## Problem Statement
- **High latency** due to centralized inference servers.
- **Inconsistencies in output** when models are updated.
- **Lack of resilience** in current system designs.

## Objective & Scope
- Build a **low-latency system** via geographically distributed replicas.
- Ensure **model consistency** using a custom implementation of the **Raft consensus algorithm**.
- Use **Model Context Protocol (MCP)** to route inference requests to the appropriate model (tentative understanding).
- Learn and apply **Terraform** for infrastructure as code and **auto-scaling containers** (final stage of development).

## User Stories:
### Host
- Should be able to deploy machine learning models to different locations.
- Update the model (we have to take care of stale outputs here)
- Delete the model
- Keep a centralized log of the users
- Have a dashboard view of the things

### User
- Should be able to put queries routed to the appropriate model as set by the Host.

## Basic Architecture

### Model Containers
- ML models are **containerized using Docker**.
- Deployed across multiple **AWS regions**.
- Serve predictions via **FastAPI** or similar lightweight backends.

### Model Controller + Raft
- A **custom-built Raft module** handles:
  - Leader election
  - Log replication for model update propagation
  - Version synchronization across replicas

### Load Balancer (Custom)
- Uses **Model Context Protocol (MCP)** to:
  - Route inference requests to the **nearest geographical node**
  - Ensure requests are served by the **correct model version**
    
### Infrastructure Layer
- **Terraform** automates cloud resource provisioning.
- Deployed on **AWS ECS or EC2** with **auto-scaling groups**.
