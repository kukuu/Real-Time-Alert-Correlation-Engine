# End-to-End Software Development Cycle Documentation

LE Alert Correlation System

1. Technology Stack

**Backend (Java)**
 - Framework: Spring Boot 3.x
 - Build Tool: Maven
 - Java Version: 17+
 - Database: PostgreSQL / H2 (development)
 - Security: Spring Security, JWT
 - Real-time: WebSocket (STOMP)
 - Messaging: Apache Kafka (for future scaling)
 - API Documentation: OpenAPI 3.0 / Swagger
 - Testing: JUnit 5, Mockito, TestContainers

**Frontend (React)**
- Framework: React 18 with TypeScript
- Build Tool: Vite
- Styling: Tailwind CSS + CSS Modules
- State Management: React Context + Hooks
- HTTP Client: Axios
- Real-time: WebSocket Client
- Routing: React Router v6
- Validation: Zod
- Testing: Jest, React Testing Library, Cypress

**DevOps & Tools**
- Version Control: Git
- Containerization: Docker
- CI/CD: GitHub Actions

**Monitoring: Prometheus + Grafana (future)**
- Logging: ELK Stack (future)

