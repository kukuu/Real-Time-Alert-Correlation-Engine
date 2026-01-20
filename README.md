# Law Enforcement Real Time Alert Correlation Engine
 
This system is designed for high availability, scalability, and maintainability, suitable for law enforcement (LE) and critical incident management (CIM) scenarios. 

The LE Alert Correlation System  consumes multiple Kafka streams (e.g., 911 calls, social media keywords, sensor alerts), uses geospatial libraries to correlate by location, and flags potential critical incidents. 

The  system follows a structured end-to-end development cycle that begins with establishing a secure, real-time communication pipeline between the Java Spring Boot backend and the React TypeScript frontend. The backend is built around a correlation engine that processes alerts through services like `CorrelationService` and `RuleEngine`, while the frontend leverages React Context and custom hooks for state management. Authentication is handled via JWT tokens, with Spring Security on the backend and protected routes on the frontend ensuring that only authorized personnel can access sensitive alert data. The entire flow is initialized through environment-specific configurations, Maven for backend builds, and Vite for frontend tooling, with startup scripts enabling seamless local and production deployment. 

Data flows through a well-defined sequence: alerts ingested via REST APIs trigger backend processing, correlation logic, and real-time WebSocket broadcasts to connected frontend clients. Middleware such as security filters, CORS policies, and audit logs intercept each request, ensuring compliance and monitoring. The frontend subscribes to WebSocket channels via the `useWebSocket` hook, updating global state through contexts like `AlertContext`, which then re-renders components such as the Dashboard and IncidentMap. This bidirectional, event-driven architecture ensures that field operators receive instantaneous updates while maintaining a persistent, secure connection between services. 

The development and deployment pipeline incorporates robust DevOps practices, including CI/CD via GitHub Actions, Docker containerization, and comprehensive testing strategies. Backend unit tests with JUnit and frontend integration tests with React Testing Library validate functionality, while security scans and linting enforce code quality. Environment configurations—such as `application.yml` for Spring profiles and `.env` files for frontend variables—allow the system to adapt across development, staging, and production environments. Utility scripts and Makefile commands streamline build processes, ensuring consistent and repeatable deployments.

To mitigate risks and plan for growth, the architecture includes safeguards such as WebSocket reconnection strategies, database indexing, encryption for PII, and regular security audits. Future enhancements may introduce machine learning for anomaly detection, microservices for scalability, and mobile applications for field operations. This forward-looking approach ensures the system remains resilient, compliant with law enforcement standards, and capable of evolving to meet emerging operational demands while maintaining high availability and real-time performance.


 ![image](https://github.com/kukuu/Real-Time-Alert-Correlation-Engine/blob/main/le-snapsots/le-1.png)

![image](https://github.com/kukuu/Real-Time-Alert-Correlation-Engine/blob/main/le-snapsots/le-2.png)

![image](https://github.com/kukuu/Real-Time-Alert-Correlation-Engine/blob/main/le-snapsots/le-3.png)

![image](https://github.com/kukuu/Real-Time-Alert-Correlation-Engine/blob/main/le-snapsots/le-4.png)

![image](https://github.com/kukuu/Real-Time-Alert-Correlation-Engine/blob/main/le-snapsots/le-5.png)

  ### ⚠️ LAW ENFORCEMENT SPECIFIC CONSIDERATIONS

- Critical Requirements:
  - Data Sovereignty: LE data must not leave jurisdiction
  - Chain of Custody: Complete audit trail for all alerts
  - Access Control: Multi-factor authentication + RBAC
  - Data Retention: Specific periods for different alert types
  - Emergency Override: Manual intervention capabilities
 
 ## End-to-End Software Development Cycle 
 
 
 ## CI/CD Workflow

 https://github.com/kukuu/Real-Time-Alert-Correlation-Engine/blob/main/development-pipeline-CI-CD-workflow.md

 ## Features 

 - Authentication (with mock login)

- Routing with protected routes 

- Dashboard with stats

- Alerts page with table
 
- Map page with Leaflet integration

- Incidents page

- Responsive design (with Tailwind CSS)

- TypeScript for type safety

- React Query for data fetching

- Context API for state management

 ## Data Flow Summary: Java Backend to React Frontend

 ### Implementation overview
 This implementation provides:

- Full-stack architecture with clear separation between frontend and backend

- Real-time data flow from Kafka through Java services to React

- Security-first approach with JWT, encryption, and audit logging

- React patterns with hooks, context, and TypeScript

- Production-ready configuration with Docker, monitoring, and deployment scripts

- Comprehensive error handling and user experience considerations

- Performance optimizations including code splitting, caching, and PWA support

 ### Data Flow Architecture

https://github.com/kukuu/Real-Time-Alert-Correlation-Engine/blob/main/architecture.md

### Data Flow Steps

#### Phase 1: Ingestion (Java Backend)

```
1. External Data Sources → Ingestor Services
   • 911 calls via SIP/REST webhooks
   • Social media via Twitter/Facebook APIs
   • Sensors via MQTT/HTTP
   • Other sources via adapters

2. Ingestor Services → Kafka
   • Data normalized to common Alert schema (Avro)
   • PII encrypted using AES-256-GCM
   • Geolocation enrichment using GeoIP/OSM
   • Published to partitioned Kafka topics

3. Kafka → Correlation Engine
   • Stream processing with Kafka Streams/Quarkus
   • Geospatial clustering using JTS/GeoTools
   • Rule evaluation using Drools
   • ML inference via TensorFlow Serving
```
#### Phase 2: Processing & Storage (Java Backend)

```
4. Correlation Engine → Storage
   • Correlated incidents saved to MongoDB
   • Audit logs to PostgreSQL
   • Cached data to Redis
   • File attachments to S3/MinIO

5. Storage → Alert Service
   • REST APIs expose processed data
   • WebSocket server for real-time push
   • Security layer validates JWT tokens
   • Rate limiting per user/department
```
#### Phase 3: Frontend Integration (React)

```
6. Alert Service → React Frontend (HTTP)
   • Initial page load: index.html + React bundle
   • Authentication: OAuth2/OIDC flow
   • Data fetching: REST APIs with Axios
   • File uploads: Multipart/form-data

7. Alert Service → React Frontend (WebSocket)
   • Real-time alerts: STOMP over WebSocket
   • Live location updates: GeoJSON streams
   • User presence: Heartbeat/ping
   • Notifications: Browser Push API

8. React State Management
   • Context API for global state (auth, alerts)
   • React Query for server state caching
   • Local state for UI interactions
   • IndexedDB for offline storage
```

#### Phase 4: User Interaction & Feedback Loop

```
9. User Actions → Backend
   • Alert acknowledgements → PATCH /api/alerts/{id}
   • Incident creation → POST /api/incidents
   • Report generation → POST /api/reports
   • User management → Admin APIs

10. Backend → External Systems
    • Dispatch integration → CAD/RMS systems
    • Notification services → Email/SMS/Push
    • Reporting → BI tools (Tableau, PowerBI)
    • Archival → Cold storage (S3 Glacier)
```

## Key Integration Points
This integrated architecture ensures seamless data flow between Java backend services and the React frontend, with proper security, scalability, and real-time capabilities throughout the system.
### HTTP API Integration:

```
React → Spring Cloud Gateway → Microservices
• RESTful APIs with OpenAPI 3.0 specifications
• Request/Response transformation at gateway
• Circuit breaker pattern for resilience
• Distributed tracing with correlation IDs
```

### WebSocket Integration:
```

React ←→ Alert Service (Spring WebSocket)
• STOMP protocol over WebSocket
• Authentication via JWT in handshake
• Subscription-based topics per user/jurisdiction
• Automatic reconnection with exponential backoff

```

### Event Streaming Integration:

```
Java Services → Kafka → React (via WebSocket)
• Real-time alerts published to Kafka
• Correlation engine processes streams
• Results pushed via WebSocket to React
• React components update in real-time
```

### Security Integration:

```
React ← OAuth2/OIDC → Auth Service
• JWT tokens issued by Auth service
• React stores tokens in secure HTTP-only cookies
• Token refresh handled automatically
• Role-based access control enforced at API gateway
```

### Data Synchronization:
```
React ← HTTP/WebSocket → Backend Services
• Initial data load via HTTP REST APIs
• Real-time updates via WebSocket
• Offline support with IndexedDB
• Conflict resolution on reconnection
```

### Security & Compliance Implementation

#### CJIS Compliance Measures:
- Data Encryption: All PII encrypted at rest using AES-256-GCM

- Access Control: RBAC with mandatory 2FA for all users

- Audit Trail: Immutable audit logs with cryptographic signatures

- Network Security: TLS 1.3, mutual TLS for service-to-service communication

- Key Management: HashiCorp Vault for secrets management

#### Operational Security:
-Zero Trust Architecture: No implicit trust, verify all requests

- Defense in Depth: Multiple security layers at network, application, and data levels

- Real-time Monitoring: Security events monitored 24/7

- Incident Response: Automated playbooks for security incidents

#### Data Handling:
- Data Minimization: Only collect necessary data

- Retention Policies: Automatic data purging per policy

- Chain of Custody: Digital evidence handling procedures

- Cross-jurisdiction Compliance: Configurable rules per region

### Deployment & Operations

#### CI/CD Pipeline:
- Security Scanning: SAST, DAST, dependency scanning in pipeline

- Compliance Checks: Automated policy validation

- Immutable Infrastructure: Infrastructure as Code with Terraform

- Blue-Green Deployments: Zero-downtime updates

#### Monitoring & Observability:
- Distributed Tracing: Jaeger for request tracking

- Metrics: Prometheus with LE-specific dashboards

- Logging: ELK stack with encrypted logs

- Alerting: PagerDuty integration for critical incidents


## Deployment Constraints:
- On-premise deployment often required
- Air-gapped environments possible
- Strict change management procedures
- Mandatory penetration testing pre-deployment
- LE personnel security clearance for operations

## Folder Structure

https://github.com/kukuu/Real-Time-Alert-Correlation-Engine/blob/main/folder-structure.md

## Code Repository 
- https://github.com/kukuu/JAVA/tree/main (**PRIVATE**)

