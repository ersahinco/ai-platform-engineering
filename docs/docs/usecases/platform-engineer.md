---
sidebar_position: 1
---

# Use-case: Platform Engineer

## Overview

Platform Engineers focus on building and maintaining the foundational infrastructure and tools that enable software development teams to deliver applications efficiently. They ensure scalability, reliability, and automation across the platform.

## Key Responsibilities

- **Infrastructure Management**: Design, implement, and manage cloud or on-premises infrastructure.
- **Automation**: Develop CI/CD pipelines and automate repetitive tasks to improve efficiency.
- **Monitoring and Observability**: Implement monitoring tools to ensure system health and performance.
- **Collaboration**: Work closely with developers, SREs, and other stakeholders to align platform capabilities with business needs.

## Tools and Technologies

- **Containerization**: Docker, Kubernetes
- **Cloud Providers**: AWS, Azure, Google Cloud
- **CI/CD**: Jenkins, GitHub Actions, CircleCI
- **Monitoring**: Prometheus, Grafana, ELK Stack

## Benefits of the Role

- Improved developer productivity through streamlined workflows.
- Enhanced system reliability and scalability.
- Faster delivery of features and updates.

## Example Use-case

A Platform Engineer designs a Kubernetes-based infrastructure to support microservices architecture, automates deployments using Helm charts, and integrates monitoring tools like Prometheus and Grafana to ensure system observability.

## Getting Started

Use the maintained CAIPE startup paths rather than persona-specific generated compose files:

```bash
# Standard local runtime
docker compose --profile caipe-ui up

# Development runtime
docker compose -f docker-compose.dev.yaml --profile caipe-ui up --build
```

### Available Personas

- **platform-engineer**: Complete setup with ArgoCD, AWS, Backstage, Confluence, GitHub, Jira, Komodor, PagerDuty, Slack, Splunk, Weather, Webex, and Petstore agents
- **devops-engineer**: DevOps-focused setup with ArgoCD, AWS, GitHub, Jira, Komodor, and PagerDuty agents
- **caipe-basic**: Minimal setup with Weather and Petstore agents for getting started

These personas describe useful agent combinations conceptually, but the old persona-based compose generator is not a maintained workflow in this repository.

Use [Docker Compose setup](../getting-started/docker-compose/setup.md) for local runtime, and [Repository Mental Model](../contributing/repository-mental-model.md) for repo ownership and layout context.
