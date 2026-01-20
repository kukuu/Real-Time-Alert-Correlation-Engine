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
**3.4 Component Hierarchy**

```
App.tsx
├── ProtectedRoute.tsx
│   ├── Header.tsx
│   ├── Sidebar.tsx
│   └── Page Content
│       ├── DashboardPage.tsx
│       ├── AlertsPage.tsx
│       ├── IncidentsPage.tsx
│       └── MapPage.tsx

```
### Phase 4: Integration & Data Flow
**4.1 API Communication**
```
// alertService.ts
const alertService = {
  // HTTP Requests
  getAlerts: () => axios.get(`${API_URL}/alerts`),
  createAlert: (alert) => axios.post(`${API_URL}/alerts`, alert),
  
  // WebSocket
  subscribeToAlerts: (callback) => {
    const ws = new WebSocket(WS_URL);
    ws.onmessage = (event) => callback(JSON.parse(event.data));
  }
};
```
**4.2 Middleware Chain (Backend)**

```
HTTP Request → SecurityFilter → CORSFilter → LoggingFilter → Controller
         ↓
Authentication → Authorization → Business Logic → Response
         ↓
Audit Logging → Database Persistence → WebSocket Broadcast
```
**4.3 Real-time Data Pipeline**

```
1. New Alert Created → POST /api/alerts
2. Backend Processes → CorrelationService.correlate()
3. Database Save → AlertRepository.save()
4. Kafka Event → alert.created (future)
5. WebSocket Broadcast → /topic/alerts
6. Frontend Receives → useWebSocket hook
7. Context Update → AlertContext.setAlerts()
8. UI Re-render → Components update
```
## 3. Configuration Files

**Backend Configuration**

```
backend/
├── pom.xml                    # Maven dependencies
├── src/main/resources/
│   ├── application.yml       # Spring configuration
│   ├── application-dev.yml   # Development config
│   ├── application-prod.yml  # Production config
│   ├── schema.sql           # Database schema
│   └── data.sql             # Initial data`

```
_application.yml example:_

```

spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/le_alerts
    username: ${DB_USERNAME}
    password: ${DB_PASSWORD}
  jpa:
    hibernate:
      ddl-auto: update
      
server:
  port: 8080
  
security:
  jwt:
    secret: ${JWT_SECRET}
    expiration: 86400000
```
**Frontend Configuration**

```
frontend/
├── vite.config.ts            # Build configuration
├── tailwind.config.js       # Styling configuration
├── tsconfig.json           # TypeScript configuration
├── package.json            # Dependencies & scripts
└── .env                    # Environment variables

```
_package.json_

```
{
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "preview": "vite preview",
    "test": "jest",
    "lint": "eslint . --ext ts,tsx",
    "start-backend": "cd ../backend && mvn spring-boot:run",
    "start": "concurrently \"npm run start-backend\" \"npm run dev\""
  }
}
```

## 4. Startup & Execution Scripts

**4.1 Development Startup**

```
# Initial setup
./scripts/setup-dev.sh

```
```
# Start both services (using Makefile)
make dev-start
```
```
# Or manually:
# Terminal 1: Backend
cd backend
mvn spring-boot:run -Dspring.profiles.active=dev
```
```
# Terminal 2: Frontend
cd frontend
npm run dev

```
**4.2 Production Build**

```
# Build both applications
make build-all
```
```
# Backend build
cd backend
mvn clean package -DskipTests
# Output: target/real-time-alert-correlation-engine.jar
```
```
# Frontend build
cd frontend
npm run build
# Output: dist/ directory
```
**4.3 Docker Integration**
```
# Dockerfile.backend
FROM openjdk:17-jdk-slim
COPY target/*.jar app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```

```
# Dockerfile.frontend
FROM nginx:alpine
COPY dist/ /usr/share/nginx/html
COPY nginx.conf /etc/nginx/nginx.conf
```
## 5. API Contract & Data Flow
_Authentication:_
```
  POST   /api/auth/login     → Login with credentials
  POST   /api/auth/refresh   → Refresh JWT token
  POST   /api/auth/logout    → Invalidate token
```
```
Alerts:
  GET    /api/alerts         → List alerts with filters
  POST   /api/alerts         → Create new alert
  GET    /api/alerts/{id}    → Get specific alert
  PUT    /api/alerts/{id}    → Update alert
  DELETE /api/alerts/{id}    → Delete alert
```
```
Incidents:
  GET    /api/incidents      → List correlated incidents
  POST   /api/incidents      → Create incident from alerts
```
