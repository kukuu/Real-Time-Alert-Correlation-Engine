# Development Pipeline and CI/CD Workflow 

## Law Enforcement Real-Time Alert Correlation System.

### 📊 SYSTEM ARCHITECTURE OVERVIEW

- Core Components:
  - Frontend - React app (Port 3000)
  - API Gateway - Spring Boot (Port 8080)
  - Microservices - Alert Service + Correlation Engine
  - Data Stores - MongoDB, PostgreSQL, Redis
  - Message Bus - Kafka + Schema Registry
  - Monitoring - Prometheus + Grafana + Jaeger
  - Service Discovery - Eureka
  - Configuration - Spring Config Server

### 🔧 **DEVELOPMENT PIPELINE (SDLC)**

 - Phase 1: Local Development
   - Frontend: docker-compose up frontend (Vite dev server)
   - Backend: Services built with Docker Compose
   - Database: Pre-initialized with law enforcement schemas
   -  Message Queue: Kafka topics auto-created
   -  Testing: Unit tests run before container startup

```
Dependencies: Docker, Node.js 18+, Java 17+, Maven/Gradle
Outcome: Full local stack running with hot-reload
```



