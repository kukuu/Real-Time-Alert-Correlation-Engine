# End-to-End Software Development Cycle Documentation

LE Alert Correlation System

## Technology Stack

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

## 2. Development Cycle Sequence

### Phase 1: Project Initialization**

```
# Backend Initialization
mvn archetype:generate \
  -DgroupId=com.le \
  -DartifactId=real-time-alert-correlation-engine \
  -DarchetypeArtifactId=maven-archetype-quickstart \
  -DinteractiveMode=false
```
```
# Frontend Initialization
npm create vite@latest frontend -- --template react-ts
```

### Phase 2: Backend Development Sequence**

**2.1 Database & Models Setup**

  - Schema Definition (src/main/resources/schema.sql)
    - Entity Models (src/main/java/com/le/correlation/model/)
    - Alert.java - Core alert entity
    - AlertCluster.java - Grouped alerts
    - CorrelatedIncident.java - Incident entity

  - Repository Layer (Spring Data JPA)

**2.2 Service Layer Development**
```
// Execution Sequence:
1. CorrelationService.java → Main correlation logic
2. RuleEngine.java → Business rule processing
3. GeospatialService.java → Location-based correlation
4. ThreatIntelligenceService.java → External threat data
```

**2.3 API Controllers**
```
@RestController
@RequestMapping("/api/alerts")
public class AlertController {
    // GET /api/alerts → AlertService.getAlerts()
    // POST /api/alerts → AlertService.createAlert()
    // WebSocket /ws/alerts → Real-time updates
}
```

**2.4 Security Implementation**
```
// SecurityConfig.java
@Configuration
@EnableWebSecurity
public class SecurityConfig {
    // JWT Authentication Filter
    // CORS Configuration
    // Role-based Authorization
    // Audit Logging
}
```

### Phase 3: Frontend Development Sequence

**3.1 Environment Setup**

```
# .env
VITE_API_URL=http://localhost:8080/api
VITE_WS_URL=ws://localhost:8080/ws
VITE_APP_NAME=LE-Alert-System
VITE_ENVIRONMENT=development
```

**3.2 Authentication Flow**

```
// Sequence: Login → Token Storage → API Calls
1. Login.tsx → POST /api/auth/login
2. AuthContext.tsx → Store JWT token
3. useAuth.ts → Token validation
4. ProtectedRoute.tsx → Route guarding
```

**3.3 Data Flow Architecture**
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   WebSocket     │    │   API Service   │    │    Context      │
│   (useWebSocket)│────▶  (alertService) │────▶  (AlertContext) │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  Real-time      │    │   Components    │    │     Pages       │
│   Updates       │    │  (Dashboard.tsx)│    │(DashboardPage.tsx)│
└─────────────────┘    └─────────────────┘    └─────────────────┘
```
