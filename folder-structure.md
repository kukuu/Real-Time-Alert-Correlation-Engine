# Folder Structure

## Phase 1

```

le-alert-correlation-system/
├── 📁 frontend/
│   ├── public/
│   │   └── index.html
│   ├── src/
│   │   ├── components/
│   │   │   ├── common/
│   │   │   │   └── LoadingSpinner.tsx
│   │   │   ├── dashboard/
│   │   │   │   └── Dashboard.tsx
│   │   │   ├── layout/
│   │   │   │   ├── Header.tsx
│   │   │   │   ├── Sidebar.tsx
│   │   │   │   └── ProtectedRoute.tsx
│   │   │   └── map/
│   │   │       └── IncidentMap.tsx
│   │   ├── contexts/
│   │   │   ├── AuthContext.tsx
│   │   │   └── AlertContext.tsx
│   │   ├── hooks/
│   │   │   ├── useAuth.ts
│   │   │   └── useWebSocket.ts
│   │   ├── pages/
│   │   │   ├── Login.tsx
│   │   │   ├── DashboardPage.tsx
│   │   │   ├── AlertsPage.tsx
│   │   │   ├── IncidentsPage.tsx
│   │   │   └── MapPage.tsx
│   │   ├── services/
│   │   │   └── api/
│   │   │       └── alertService.ts
│   │   ├── styles/
│   │   │   ├── global.css
│   │   │   └── theme.tsx
│   │   ├── types/
│   │   │   └── index.ts
│   │   ├── utils/
│   │   │   ├── constants.ts
│   │   │   └── formatters.ts
│   │   ├── App.tsx
│   │   └── index.tsx
│   ├── package.json
│   ├── package-lock.json
│   ├── tsconfig.json
│   ├── tsconfig.node.json
│   ├── vite.config.ts
│   ├── tailwind.config.js
│   └── postcss.config.js
├── 📁 backend/
│   ├── common/
│   │   ├── data-models/
│   │   │   └── src/main/java/com/le/models/
│   │   │       └── Alert.java
│   │   └── security-core/
│   │       └── src/main/java/com/le/security/
│   │           └── SecurityConfig.java
│   ├── src/main/java/com/le/correlation/
│   │   ├── model/
│   │   │   ├── Alert.java
│   │   │   ├── AlertCluster.java
│   │   │   ├── AlertSource.java
│   │   │   ├── CorrelatedIncident.java
│   │   │   ├── IncidentEvaluation.java
│   │   │   ├── Priority.java
│   │   │   └── Severity.java
│   │   └── service/
│   │       ├── CorrelationService.java
│   │       ├── GeospatialService.java
│   │       ├── ThreatIntelligenceService.java
│   │       └── RuleEngine.java
│   ├── target/
│   │   └── classes/com/le/correlation/
│   │       └── model/
│   │           └── (compiled classes)
│   └── pom.xml
├── 📁 docs/
│   └── README.md
├── .gitignore
├── README.md
└── package.json (frontend root)

```

