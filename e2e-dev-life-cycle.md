# Documentation: End-to-End Software Development Cycle 

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

**5.1 REST API Endpoints**
_Authentication:_
```
  POST   /api/auth/login     → Login with credentials
  POST   /api/auth/refresh   → Refresh JWT token
  POST   /api/auth/logout    → Invalidate token
```
_Alerts:_
```
  GET    /api/alerts         → List alerts with filters
  POST   /api/alerts         → Create new alert
  GET    /api/alerts/{id}    → Get specific alert
  PUT    /api/alerts/{id}    → Update alert
  DELETE /api/alerts/{id}    → Delete alert
```
_Incidents:_
```
  GET    /api/incidents      → List correlated incidents
  POST   /api/incidents      → Create incident from alerts
```
**5.2 WebSocket Channels**

_STOMP Endpoints:_
```
  /ws                         → WebSocket connection
  /app/alerts                 → Send alert updates
  /topic/alerts               → Subscribe to alerts
  /topic/incidents            → Subscribe to incidents
```  
_Message Format:_
```
{
  "type": "ALERT_CREATED",
  "payload": {...},
  "timestamp": "2024-01-15T10:30:00Z"
}

```
**5.3 Data Models Synchronization**

```
// types/index.ts (Frontend)
interface Alert {
  id: string;
  source: '911' | 'SENSOR' | 'SOCIAL_MEDIA';
  priority: 'LOW' | 'MEDIUM' | 'HIGH';
  category: string;
  location: {
    lat: number;
    lng: number;
    address: string;
  };
  timestamp: string;
}

// Alert.java (Backend)
@Entity
public class Alert {
    @Id
    @GeneratedValue(strategy = GenerationType.UUID)
    private String id;
    
    @Enumerated(EnumType.STRING)
    private AlertSource source;
    
    @Enumerated(EnumType.STRING)
    private Priority priority;
    
    private String category;
    
    @Embedded
    private Location location;
    
    private Instant timestamp;
}
```

## 6. Security Implementation

**6.1 Authentication Flow**

```
1. Frontend: Login form submission
2. Backend: Validate credentials → Generate JWT
3. Frontend: Store token in localStorage (with encryption)
4. Subsequent requests: Add Authorization header
5. Backend: Validate JWT on each request
6. WebSocket: Send token in connection header
```

**6.2 Security Best Practices**
```
// Backend SecurityConfig.java
@Configuration
@EnableWebSecurity
public class SecurityConfig {
    
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        return http
            .cors(Customizer.withDefaults())
            .csrf(AbstractHttpConfigurer::disable)
            .sessionManagement(session -> session
                .sessionCreationPolicy(SessionCreationPolicy.STATELESS))
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/api/auth/**").permitAll()
                .requestMatchers("/ws/**").permitAll()
                .requestMatchers("/api/admin/**").hasRole("ADMIN")
                .anyRequest().authenticated())
            .addFilterBefore(jwtFilter, UsernamePasswordAuthenticationFilter.class)
            .build();
    }
}
```

**6.3 Frontend Security**
```
// ProtectedRoute.tsx
const ProtectedRoute = ({ children }: { children: ReactNode }) => {
  const { isAuthenticated } = useAuth();
  
  if (!isAuthenticated) {
    return <Navigate to="/login" replace />;
  }
  
  return children;
};

// HTTP Interceptor for adding tokens
axios.interceptors.request.use((config) => {
  const token = localStorage.getItem('auth_token');
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});
```
## 7. Testing Strategy


**Risk	                                   Impact	                           Mitigation**
Real-time data loss                      	High	                             Implement WebSocket reconnection with backoff
Database performance	Medium	Add indexing, caching (Redis), query optimization
Security breaches	Critical	Regular security audits, penetration testing
Frontend state sync issues	Medium	Implement optimistic updates, offline storage
API rate limiting	Low	Implement circuit breaker pattern

**7.1 Backend Testing**
```
@SpringBootTest
@AutoConfigureMockMvc
class AlertControllerTest {
    
    @Test
    void createAlert_ValidInput_ReturnsCreated() {
        AlertDto alertDto = new AlertDto(...);
        
        mockMvc.perform(post("/api/alerts")
                .contentType(MediaType.APPLICATION_JSON)
                .content(objectMapper.writeValueAsString(alertDto)))
                .andExpect(status().isCreated());
    }
}
```

**7.2 Frontend Testing**
```
// Dashboard.test.tsx
describe('Dashboard', () => {
  it('displays alert statistics', async () => {
    render(<Dashboard />);
    
    expect(await screen.findByText('Total Alerts')).toBeInTheDocument();
    expect(screen.getByText('1,234')).toBeInTheDocument();
  });
});
```

**7.3 Integration Testing**

```
# Run complete test suite
make test-all
```
```
# Backend tests
cd backend && mvn test
```
```
# Frontend tests
cd frontend && npm test
```
```
# E2E tests
npm run cypress:open
```
## 8. Deployment Pipeline

**8.1 CI/CD Workflow (.github/workflows)**
```
# frontend-ci.yml
name: Frontend CI

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
      - run: npm ci
      - run: npm run build
      - run: npm run test
      - run: npm run lint
```

**8.2 Build Pipeline**
```
1. Code Commit → Git Push
2. GitHub Actions Trigger
3. Install Dependencies (npm ci / mvn install)
4. Run Tests (Unit + Integration)
5. Build Artifacts
6. Security Scan (SonarQube)
7. Docker Image Build
8. Push to Container Registry
9. Deploy to Environment
```

## Monitoring & Observability
**9.1 Logging Strategy**

```
// Backend logging
@Slf4j
@Service
public class CorrelationService {
    
    public Alert correlateAlerts(List<Alert> alerts) {
        log.info("Starting correlation for {} alerts", alerts.size());
        // Correlation logic
        log.debug("Correlation result: {}", result);
        auditService.logEvent("ALERT_CORRELATED", user, result);
    }
}
```

**9.2 Frontend Monitoring**

```
// Error boundary for React
class ErrorBoundary extends React.Component {
  componentDidCatch(error: Error, errorInfo: React.ErrorInfo) {
    logErrorToService(error, errorInfo);
    // Send to monitoring service
    monitoringService.captureException(error);
  }
}
```
## 10. Risk Factors & Mitigation

**10.1 Technical Risks**

Risk	                           Impact                   	Mitigation


Real-time data loss            	High	                    Implement WebSocket reconnection with backoff


Database performance	Medium	Add indexing, caching (Redis), query optimization
Security breaches	Critical	Regular security audits, penetration testing
Frontend state sync issues	Medium	Implement optimistic updates, offline storage
API rate limiting	Low	Implement circuit breaker pattern
