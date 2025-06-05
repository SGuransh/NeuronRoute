# RFP: Distributed Sentiment Intelligence Platform for Companies

## Project Title
**NeuronRoute v2: Distributed Sentiment Analysis Dashboard for Companies**

## Background
Traditional market feedback loops are slow and reactive. In an era where public sentiment evolves in real-time on social platforms like Twitter and Reddit, companies need a proactive, scalable, and resilient solution to monitor and act on public opinion. NeuronRoute aims to fill this gap by leveraging distributed infrastructure and machine learning to deliver high-availability sentiment insights.

## Problem Statement
- Companies lack real-time visibility into public sentiment surrounding their products.
- Existing solutions are either centralized, slow, or not domain-customizable.
- Categorizing and diagnosing issues like "price dissatisfaction" or "design flaws" from user posts remains unstructured and ad hoc.

## Objectives
- Build a distributed, real-time ETL and inference platform.
- Allow companies to subscribe and configure the accounts, topics, or products they want to track.
- Perform sentiment analysis and reason categorization (e.g., pricing, appearance, reliability).
- Provide an interactive dashboard with:
  - Sentiment trends over time.
  - Top positive/negative posts.
  - Breakdown of criticism reasons.
  - Alerts for sentiment dips or spikes.
- Ensure high-availability and fault tolerance using distributed techniques (e.g., Raft).

## Scope

### ETL Pipeline
- Custom-built scrapers to collect and clean data from Reddit, Twitter, and other public sources.

### Model Layer
- Deploy transformer-based models for sentiment and category classification.

### Distributed Infra
- Models replicated across regions.
- Custom Raft module to sync category model updates.
- MCP for inference routing based on geo and version.

### Frontend
- Company-facing dashboards (with drill-down by product, time, and issue).

### Admin Panel
- Configure data sources per client.
- View system usage and logs.

### Auto-scaling Infra
- Use Terraform to provision ECS/EC2 with auto-scaling and observability (e.g., Grafana).

## User Stories

### As a Company (Client)
- I want to subscribe to the platform and configure which accounts/products to track.
- I want to view public sentiment over time.
- I want to know why people dislike or love my product (price, UX, quality, etc.).
- I want to be alerted when there's a surge in negative sentiment.

### As a Platform Admin
- I want to deploy models across regions with Raft-synced updates.
- I want to log user interactions and sentiment spikes.
- I want to manage client access and dashboard provisioning.
- I want to run inference at low latency from the nearest replica node.

## Deliverables
- Distributed ETL + sentiment inference system.
- MCP-based load balancer.
- Raft module for version sync.
- Terraform-based cloud provisioning.
- Real-time dashboard for clients.

## Tech Stack (Tentative)
- **Backend**: Python (FastAPI), Go (Raft module)
- **Frontend**: React.js + Tailwind
- **ML**: HuggingFace Transformers (BERT/Sentiment Models), Custom Classifier for Issue Categorization
- **Infra**: Docker, AWS ECS/EC2, Terraform, Prometheus, Grafana
- **Data Sources**: Custom scrapers for Reddit, Twitter, and other public data platforms
