# Config Repo

Centralized Git repository for Spring Cloud Config Server configuration files in the EventSphere microservices platform.

## Overview

This repository contains all externalized configuration YAML files for the EventSphere backend microservices. The Spring Cloud Config Server reads configuration directly from this repository and serves it to client services at runtime.

## Configuration Files

| File | Service | Description |
|------|---------|-------------|
| `eureka-server.yml` | Eureka Server | Service discovery registry configuration |
| `config-server.yml` | Config Server | Git-backed configuration server settings |
| `api-gateway.yml` | API Gateway | Routing rules, CORS, resilience, and load balancing |
| `user-service.yml` | User Service | Database connection, JPA, and Eureka client settings |
| `event-booking-service.yml` | Event Booking Service | Database connection, JPA, and Eureka client settings |
| `review-notification-service.yml` | Review & Notification Service | GCP project settings, Firestore, and Cloud Storage |

## Repository Structure

```
config-repo/
├── README.md
├── eureka-server.yml
├── config-server.yml
├── api-gateway.yml
├── user-service.yml
├── event-booking-service.yml
└── review-notification-service.yml
```

## Usage

The Spring Cloud Config Server is configured to fetch configuration from this repository:

```
Server URL: https://github.com/Dinidu21/config-repo.git
```

Services access their configuration at:

```
http://<config-server-host>:8888/<application-name>/<profile>
```

## Configuration Profiles

All services currently use the `default` profile.

## Secrets Management

Database passwords and sensitive credentials are injected via environment variables (e.g., `${DB_PASSWORD}`) and should not be committed to this repository.

## Updating Configuration

To update service configuration:

1. Edit the relevant YAML file in this repository
2. Commit and push changes to GitHub
3. Trigger a refresh on the target service via the Config Server or Actuator `/refresh` endpoint

## Services

| Service | Port | Database |
|---------|------|----------|
| Eureka Server | 8761 | N/A |
| Config Server | 8888 | N/A |
| API Gateway | 8080 | N/A |
| User Service | 8081 | PostgreSQL (userdb) |
| Event Booking Service | 8082 | PostgreSQL (userdb) |
| Review & Notification Service | 8083 | Google Firestore / Cloud Storage |
