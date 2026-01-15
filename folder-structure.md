# Folder Structure

```
le-alert-correlation-system/
├── 📁 .github/
│   ├── 📁 workflows/
│   │   ├── 🔹 frontend-ci.yml
│   │   ├── 🔹 backend-ci.yml
│   │   ├── 🔹 security-scan.yml
│   │   └── 🔹 deployment.yml
│   └── 🔹 dependabot.yml
├── 📁 infrastructure/
│   ├── 📁 terraform/
│   │   ├── 📁 modules/
│   │   │   ├── 📁 networking/
│   │   │   ├── 📁 kubernetes/
│   │   │   └── 📁 monitoring/
│   │   ├── 🔹 main.tf
│   │   ├── 🔹 variables.tf
│   │   └── 🔹 outputs.tf
│   ├── 📁 kubernetes/
│   │   ├── 📁 namespaces/
│   │   ├── 📁 network-policies/
│   │   ├── 📁 secrets/
│   │   └── 📁 istio/
│   ├── 📁 monitoring/
│   │   ├── 🔹 prometheus.yml
│   │   ├── 🔹 grafana-dashboards/
│   │   └── 🔹 alertmanager.yml
│   └── 📁 scripts/
│       ├── 🔹 deploy.sh
│       ├── 🔹 backup.sh
│       └── 🔹 security-audit.sh
├── 📁 frontend/                    # REACT APPLICATION
│   ├── 📁 public/
│   │   ├── 🔹 index.html
│   │   ├── 🔹 manifest.json
│   │   ├── 🔹 robots.txt
│   │   └── 📁 assets/
│   │       ├── 📁 icons/
│   │       ├── 📁 fonts/
│   │       └── 📁 images/
│   ├── 📁 src/
│   │   ├── 📁 components/
│   │   │   ├── 📁 layout/
│   │   │   │   ├── 🔹 Header.tsx
│   │   │   │   ├── 🔹 Sidebar.tsx
│   │   │   │   ├── 🔹 Footer.tsx
│   │   │   │   └── 🔹 ProtectedRoute.tsx
│   │   │   ├── 📁 alerts/
│   │   │   │   ├── 🔹 AlertList.tsx
│   │   │   │   ├── 🔹 AlertDetail.tsx
│   │   │   │   ├── 🔹 AlertFilters.tsx
│   │   │   │   └── 🔹 AlertMap.tsx
│   │   │   ├── 📁 dashboard/
│   │   │   │   ├── 🔹 Dashboard.tsx
│   │   │   │   ├── 🔹 MetricsPanel.tsx
│   │   │   │   ├── 🔹 ActivityFeed.tsx
│   │   │   │   └── 🔹 PriorityChart.tsx
│   │   │   ├── 📁 map/
│   │   │   │   ├── 🔹 IncidentMap.tsx
│   │   │   │   ├── 🔹 HeatMap.tsx
│   │   │   │   ├── 🔹 MapControls.tsx
│   │   │   │   └── 🔹 ClusterVisualization.tsx
│   │   │   ├── 📁 incidents/
│   │   │   │   ├── 🔹 IncidentList.tsx
│   │   │   │   ├── 🔹 IncidentDetail.tsx
│   │   │   │   ├── 🔹 IncidentForm.tsx
│   │   │   │   └── 🔹 IncidentTimeline.tsx
│   │   │   ├── 📁 admin/
│   │   │   │   ├── 🔹 UserManagement.tsx
│   │   │   │   ├── 🔹 AuditLog.tsx
│   │   │   │   ├── 🔹 SystemConfig.tsx
│   │   │   │   └── 🔹 RoleManager.tsx
│   │   │   └── 📁 common/
│   │   │       ├── 🔹 LoadingSpinner.tsx
│   │   │       ├── 🔹 ErrorBoundary.tsx
│   │   │       ├── 🔹 NotificationCenter.tsx
│   │   │       └── 🔹 ConfirmationDialog.tsx
│   │   ├── 📁 contexts/
│   │   │   ├── 🔹 AuthContext.tsx
│   │   │   ├── 🔹 AlertContext.tsx
│   │   │   ├── 🔹 MapContext.tsx
│   │   │   ├── 🔹 AuditContext.tsx
│   │   │   └── 🔹 WebSocketContext.tsx
│   │   ├── 📁 hooks/
│   │   │   ├── 🔹 useWebSocket.ts
│   │   │   ├── 🔹 useGeolocation.ts
│   │   │   ├── 🔹 useAuth.ts
│   │   │   ├── 🔹 useDebounce.ts
│   │   │   ├── 🔹 useLocalStorage.ts
│   │   │   └── 🔹 useOfflineDetection.ts
│   │   ├── 📁 services/
│   │   │   ├── 📁 api/
│   │   │   │   ├── 🔹 authService.ts
│   │   │   │   ├── 🔹 alertService.ts
│   │   │   │   ├── 🔹 incidentService.ts
│   │   │   │   ├── 🔹 auditService.ts
│   │   │   │   └── 🔹 geospatialService.ts
│   │   │   ├── 📁 websocket/
│   │   │   │   ├── 🔹 websocketManager.ts
│   │   │   │   ├── 🔹 stompClient.ts
│   │   │   │   └── 🔹 reconnectStrategy.ts
│   │   │   ├── 📁 storage/
│   │   │   │   ├── 🔹 indexedDB.ts
│   │   │   │   ├── 🔹 localStorage.ts
│   │   │   │   └── 🔹 cacheManager.ts
│   │   │   └── 📁 validation/
│   │   │       ├── 🔹 schemaValidators.ts
│   │   │       └── 🔹 inputSanitizers.ts
│   │   ├── 📁 utils/
│   │   │   ├── 🔹 encryption.ts
│   │   │   ├── 🔹 formatters.ts
│   │   │   ├── 🔹 constants.ts
│   │   │   ├── 🔹 security.ts
│   │   │   ├── 🔹 geospatial.ts
│   │   │   └── 🔹 dateTime.ts
│   │   ├── 📁 types/
│   │   │   ├── 🔹 index.ts
│   │   │   ├── 🔹 alert.types.ts
│   │   │   ├── 🔹 incident.types.ts
│   │   │   ├── 🔹 user.types.ts
│   │   │   ├── 🔹 geospatial.types.ts
│   │   │   └── 🔹 api.types.ts
│   │   ├── 📁 styles/
│   │   │   ├── 🔹 theme.ts
│   │   │   ├── 🔹 global.css
│   │   │   ├── 🔹 variables.css
│   │   │   └── 📁 components/
│   │   │       ├── 🔹 buttons.css
│   │   │       ├── 🔹 forms.css
│   │   │       └── 🔹 layout.css
│   │   ├── 📁 pages/
│   │   │   ├── 🔹 Login.tsx
│   │   │   ├── 🔹 DashboardPage.tsx
│   │   │   ├── 🔹 AlertsPage.tsx
│   │   │   ├── 🔹 IncidentsPage.tsx
│   │   │   ├── 🔹 MapPage.tsx
│   │   │   ├── 🔹 ReportsPage.tsx
│   │   │   ├── 🔹 AdminPage.tsx
│   │   │   └── 🔹 SettingsPage.tsx
│   │   ├── 📁 tests/
│   │   │   ├── 📁 unit/
│   │   │   ├── 📁 integration/
│   │   │   ├── 📁 e2e/
│   │   │   └── 🔹 setupTests.ts
│   │   ├── 🔹 App.tsx
│   │   ├── 🔹 index.tsx
│   │   └── 🔹 service-worker.ts
│   ├── 🔹 .env.example
│   ├── 🔹 .env.production
│   ├── 🔹 package.json
│   ├── 🔹 tsconfig.json
│   ├── 🔹 vite.config.ts
│   ├── 🔹 tailwind.config.js
│   ├── 🔹 eslint.config.js
│   ├── 🔹 Dockerfile
│   └── 🔹 README.md
├── 📁 backend/                     # JAVA MICROSERVICES
│   ├── 📁 common-lib/              # Shared libraries
│   │   ├── 📁 security-core/
│   │   │   ├── 📁 src/main/java/com/le/security/
│   │   │   │   ├── 🔹 SecurityConfig.java
│   │   │   │   ├── 🔹 JwtTokenProvider.java
│   │   │   │   ├── 🔹 EncryptionService.java
│   │   │   │   ├── 🔹 AuditService.java
│   │   │   │   └── 🔹 RateLimitService.java
│   │   │   └── 🔹 pom.xml
│   │   ├── 📁 data-models/
│   │   │   ├── 📁 src/main/java/com/le/models/
│   │   │   │   ├── 🔹 Alert.java
│   │   │   │   ├── 🔹 Incident.java
│   │   │   │   ├── 🔹 User.java
│   │   │   │   ├── 🔹 Geospatial.java
│   │   │   │   └── 🔹 AuditEvent.java
│   │   │   ├── 📁 src/main/resources/avro/
│   │   │   │   ├── 🔹 alert.avsc
│   │   │   │   └── 🔹 incident.avsc
│   │   │   └── 🔹 pom.xml
│   │   └── 📁 audit-lib/
│   │       ├── 📁 src/main/java/com/le/audit/
│   │       │   ├── 🔹 AuditAspect.java
│   │       │   ├── 🔹 AuditLogger.java
│   │       │   └── 🔹 ChainOfCustody.java
│   │       └── 🔹 pom.xml
│   ├── 📁 api-gateway/             # Spring Cloud Gateway
│   │   ├── 📁 src/main/java/com/le/gateway/
│   │   │   ├── 🔹 GatewayApplication.java
│   │   │   ├── 🔹 SecurityConfig.java
│   │   │   ├── 🔹 RateLimitFilter.java
│   │   │   ├── 🔹 JwtValidationFilter.java
│   │   │   └── 🔹 RequestLoggingFilter.java
│   │   ├── 📁 src/main/resources/
│   │   │   ├── 🔹 application.yml
│   │   │   └── 🔹 routes.yml
│   │   └── 🔹 pom.xml
│   ├── 📁 alert-service/           # Main alert service
│   │   ├── 📁 src/main/java/com/le/alerts/
│   │   │   ├── 🔹 AlertApplication.java
│   │   │   ├── 📁 controller/
│   │   │   │   ├── 🔹 AlertController.java
│   │   │   │   ├── 🔹 IncidentController.java
│   │   │   │   └── 🔹 WebSocketController.java
│   │   │   ├── 📁 service/
│   │   │   │   ├── 🔹 AlertService.java
│   │   │   │   ├── 🔹 IncidentService.java
│   │   │   │   └── 🔹 NotificationService.java
│   │   │   ├── 📁 repository/
│   │   │   │   ├── 🔹 AlertRepository.java
│   │   │   │   └── 🔹 IncidentRepository.java
│   │   │   ├── 📁 kafka/
│   │   │   │   ├── 🔹 AlertConsumer.java
│   │   │   │   └── 🔹 IncidentProducer.java
│   │   │   └── 📁 config/
│   │   │       ├── 🔹 WebSocketConfig.java
│   │   │       └── 🔹 KafkaConfig.java
│   │   ├── 📁 src/test/java/com/le/alerts/
│   │   │   └── 📁 integration/
│   │   ├── 📁 src/main/resources/
│   │   │   ├── 🔹 application.yml
│   │   │   └── 🔹 schema.sql
│   │   └── 🔹 pom.xml
│   ├── 📁 correlation-engine/      # Quarkus correlation engine
│   │   ├── 📁 src/main/java/com/le/correlation/
│   │   │   ├── 🔹 CorrelationApplication.java
│   │   │   ├── 📁 engine/
│   │   │   │   ├── 🔹 CorrelationService.java
│   │   │   │   ├── 🔹 RuleEngine.java
│   │   │   │   └── 🔹 PatternDetector.java
│   │   │   ├── 📁 geospatial/
│   │   │   │   ├── 🔹 GeospatialService.java
│   │   │   │   ├── 🔹 ClusterDetector.java
│   │   │   │   └── 🔹 DistanceCalculator.java
│   │   │   ├── 📁 ml/
│   │   │   │   ├── 🔹 AnomalyDetector.java
│   │   │   │   └── 🔹 ModelService.java
│   │   │   └── 📁 kafka/
│   │   │       ├── 🔹 AlertProcessor.java
│   │   │       └── 🔹 IncidentProducer.java
│   │   ├── 📁 src/main/resources/
│   │   │   ├── 🔹 application.properties
│   │   │   ├── 📁 rules/
│   │   │   │   ├── 🔹 correlation-rules.drl
│   │   │   │   └── 🔹 incident-rules.drl
│   │   │   └── 📁 models/
│   │   │       └── 🔹 anomaly-detection.pb
│   │   ├── 📁 src/test/java/com/le/correlation/
│   │   ├── 🔹 pom.xml
│   │   └── 🔹 Dockerfile
│   ├── 📁 geospatial-service/      # Geospatial processing
│   │   ├── 📁 src/main/java/com/le/geospatial/
│   │   │   ├── 🔹 GeospatialApplication.java
│   │   │   ├── 📁 service/
│   │   │   │   ├── 🔹 GeocodingService.java
│   │   │   │   ├── 🔹 ReverseGeocodingService.java
│   │   │   │   └── 🔹 DistanceMatrixService.java
│   │   │   ├── 📁 repository/
│   │   │   │   └── 🔹 LocationRepository.java
│   │   │   └── 📁 controller/
│   │   │       └── 🔹 GeospatialController.java
│   │   ├── 📁 src/main/resources/
│   │   │   ├── 🔹 application.yml
│   │   │   └── 📁 data/
│   │   │       └── 🔹 postal-codes.geojson
│   │   └── 🔹 pom.xml
│   ├── 📁 ingestors/               # Data ingestion services
│   │   ├── 📁 911-ingestor/
│   │   │   ├── 📁 src/main/java/com/le/ingestor/emergency/
│   │   │   │   ├── 🔹 EmergencyCallApplication.java
│   │   │   │   ├── 🔹 CallReceiverService.java
│   │   │   │   ├── 🔹 CallParserService.java
│   │   │   │   └── 🔹 KafkaPublisher.java
│   │   │   ├── 📁 src/main/resources/
│   │   │   │   └── 🔹 application.yml
│   │   │   └── 🔹 pom.xml
│   │   ├── 📁 social-media-ingestor/
│   │   │   ├── 📁 src/main/java/com/le/ingestor/social/
│   │   │   │   ├── 🔹 SocialMediaApplication.java
│   │   │   │   ├── 🔹 TwitterStreamService.java
│   │   │   │   ├── 🔹 FacebookWebhookService.java
│   │   │   │   └── 🔹 ContentAnalyzer.java
│   │   │   ├── 📁 src/main/resources/
│   │   │   │   ├── 🔹 application.yml
│   │   │   │   └── 📁 keywords/
│   │   │   │       └── 🔹 emergency-keywords.txt
│   │   │   └── 🔹 pom.xml
│   │   └── 📁 sensor-ingestor/
│   │       ├── 📁 src/main/java/com/le/ingestor/sensor/
│   │       │   ├── 🔹 SensorApplication.java
│   │       │   ├── 🔹 MqttListenerService.java
│   │       │   ├── 🔹 HttpWebhookService.java
│   │       │   └── 🔹 SensorDataProcessor.java
│   │       ├── 📁 src/main/resources/
│   │       │   └── 🔹 application.yml
│   │       └── 🔹 pom.xml
│   ├── 📁 auth-service/            # Authentication service
│   │   ├── 📁 src/main/java/com/le/auth/
│   │   │   ├── 🔹 AuthApplication.java
│   │   │   ├── 📁 controller/
│   │   │   │   ├── 🔹 AuthController.java
│   │   │   │   └── 🔹 UserController.java
│   │   │   ├── 📁 service/
│   │   │   │   ├── 🔹 UserService.java
│   │   │   │   ├── 🔹 TokenService.java
│   │   │   │   └── 🔹 MfaService.java
│   │   │   └── 📁 repository/
│   │   │       └── 🔹 UserRepository.java
│   │   ├── 📁 src/main/resources/
│   │   │   ├── 🔹 application.yml
│   │   │   └── 🔹 schema.sql
│   │   └── 🔹 pom.xml
│   ├── 📁 audit-service/           # Audit logging service
│   │   ├── 📁 src/main/java/com/le/audit/
│   │   │   ├── 🔹 AuditApplication.java
│   │   │   ├── 📁 service/
│   │   │   │   ├── 🔹 AuditLogService.java
│   │   │   │   └── 🔹 ReportService.java
│   │   │   ├── 📁 repository/
│   │   │   │   └── 🔹 AuditRepository.java
│   │   │   └── 📁 kafka/
│   │   │       └── 🔹 AuditConsumer.java
│   │   ├── 📁 src/main/resources/
│   │   │   └── 🔹 application.yml
│   │   └── 🔹 pom.xml
│   ├── 📁 config-server/           # Centralized configuration
│   │   ├── 📁 src/main/java/com/le/config/
│   │   │   └── 🔹 ConfigServerApplication.java
│   │   ├── 📁 src/main/resources/
│   │   │   ├── 🔹 application.yml
│   │   │   └── 📁 config/
│   │   │       ├── 🔹 alert-service.yml
│   │   │       ├── 🔹 correlation-engine.yml
│   │   │       └── 🔹 auth-service.yml
│   │   └── 🔹 pom.xml
│   ├── 📁 service-discovery/       # Eureka service registry
│   │   ├── 📁 src/main/java/com/le/discovery/
│   │   │   └── 🔹 DiscoveryApplication.java
│   │   ├── 📁 src/main/resources/
│   │   │   └── 🔹 application.yml
│   │   └── 🔹 pom.xml
│   └── 🔹 pom.xml                  # Parent POM
├── 📁 kafka-setup/                 # Kafka infrastructure
│   ├── 🔹 docker-compose.yml
│   ├── 🔹 kafka-config.yaml
│   ├── 🔹 schema-registry.yaml
│   └── 🔹 topics-create.sh
├── 📁 database-scripts/            # Database setup
│   ├── 📁 postgres/
│   │   ├── 🔹 init.sql
│   │   ├── 🔹 schema.sql
│   │   └── 🔹 migrations/
│   ├── 📁 mongodb/
│   │   ├── 🔹 init.js
│   │   └── 🔹 indexes.js
│   └── 📁 redis/
│       └── 🔹 config.conf
├── 📁 docs/                        # Documentation
│   ├── 📁 architecture/
│   │   ├── 🔹 data-flow.md
│   │   ├── 🔹 system-architecture.md
│   │   └── 🔹 deployment-guide.md
│   ├── 📁 api/
│   │   ├── 🔹 openapi.yaml
│   │   └── 🔹 websocket-api.md
│   ├── 📁 security/
│   │   ├── 🔹 security-model.md
│   │   ├── 🔹 compliance-checklist.md
│   │   └── 🔹 audit-requirements.md
│   ├── 📁 operations/
│   │   ├── 🔹 monitoring-guide.md
│   │   ├── 🔹 troubleshooting.md
│   │   └── 🔹 backup-recovery.md
│   └── 📁 development/
│       ├── 🔹 setup-guide.md
│       ├── 🔹 coding-standards.md
│       └── 🔹 testing-guide.md
├── 📁 scripts/                     # Utility scripts
│   ├── 📁 deployment/
│   │   ├── 🔹 build-all.sh
│   │   ├── 🔹 deploy-k8s.sh
│   │   └── 🔹 rollback.sh
│   ├── 📁 security/
│   │   ├── 🔹 generate-certs.sh
│   │   ├── 🔹 vault-init.sh
│   │   └── 🔹 security-scan.sh
│   ├── 📁 database/
│   │   ├── 🔹 backup.sh
│   │   ├── 🔹 restore.sh
│   │   └── 🔹 migrate.sh
│   └── 📁 monitoring/
│       ├── 🔹 setup-prometheus.sh
│       └── 🔹 import-dashboards.sh
├── 🔹 .gitignore
├── 🔹 .gitattributes
├── 🔹 LICENSE
├── 🔹 README.md
├── 🔹 CONTRIBUTING.md
├── 🔹 SECURITY.md
├── 🔹 CODE_OF_CONDUCT.md
├── 🔹 docker-compose.yml           # Local development
├── 🔹 Makefile                     # Common commands
└── 🔹 CHANGELOG.md
```


- Frontend updated
```
frontend/
├── public/
│   ├── index.html
│   └── vite.svg
├── src/
│   ├── components/
│   │   ├── common/
│   │   │   └── LoadingSpinner.tsx
│   │   └── layout/
│   │       ├── Header.tsx
│   │       ├── Sidebar.tsx
│   │       └── ProtectedRoute.tsx
│   ├── contexts/
│   │   ├── AuthContext.tsx
│   │   └── AlertContext.tsx
│   ├── hooks/
│   │   ├── useAuth.ts
│   │   └── useWebSocket.ts
│   ├── pages/
│   │   ├── Login.tsx
│   │   ├── DashboardPage.tsx
│   │   ├── AlertsPage.tsx
│   │   ├── IncidentsPage.tsx
│   │   └── MapPage.tsx
│   ├── styles/
│   │   ├── global.css
│   │   └── theme.tsx
│   ├── types/
│   │   └── index.ts
│   ├── utils/
│   │   ├── constants.ts
│   │   └── formatters.ts
│   ├── App.tsx
│   └── index.tsx
├── scripts/
│   └── start-dev.sh
├── .env
├── .env.example
├── .gitignore
├── index.html
├── package.json
├── package-lock.json
├── postcss.config.js
├── tailwind.config.js
├── tsconfig.json
├── tsconfig.node.json
└── vite.config.ts
```
