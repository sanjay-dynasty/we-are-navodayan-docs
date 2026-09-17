# Backend Development Details

# Phase 0 — Project & Development Setup

## B0.1 — Understand Backend Requirements

**Status:** ✅ Completed

Defined the backend architecture and initial microservice boundaries for the We Are Navodayan platform.

### Architecture

    Web / Mobile
          ↓
    API Gateway
          ↓
    Spring Boot Microservices
          ↓
    PostgreSQL / Redis / AWS

### Communication Strategy

- REST — synchronous service-to-service communication.
- Event-driven communication will be introduced when an actual asynchronous business requirement exists.

### Initial Services

- `api-gateway`
- `auth-service`
- `user-service`
- `jnv-service`
- `alumni-service`
- `community-service`
- `opportunity-service`
- `mentorship-service`
- `event-service`
- `notification-service`

### Architecture Decisions

- Each microservice owns its domain data.
- Services do not directly access another service's database.
- Services are independently deployable and scalable.
- REST is the initial communication mechanism between services.
- Kafka is deferred until an actual event-driven workflow requires it.
- Common Java base package: `com.wearenavodayan`

---

## B0.2 — Install Java & Required Tools

**Status:** ✅ Completed

Installed and configured the backend development environment.

### Tools

- Java 21 LTS
- Maven 3.9.16
- Git
- VS Code
- Docker Desktop
- Docker Compose
- WSL 2
- Ubuntu

### Configuration

Configured:

    JAVA_HOME
    MAVEN_HOME

Java 21 was configured as the active Java version.

### Verification

    java -version
    mvn -version
    git --version
    docker --version
    docker compose version
    docker run --rm hello-world

### Result

- Java 21 verified successfully.
- Maven verified successfully.
- Git verified successfully.
- Docker Engine verified successfully.
- Docker Compose verified successfully.
- Docker + WSL 2 integration verified successfully.

---

## B0.3 — Configure IDE & Development Environment

**Status:** ✅ Completed

Configured VS Code for Java and Spring Boot development.

### Installed Extensions

- Extension Pack for Java
- Language Support for Java
- Debugger for Java
- Maven for Java
- Project Manager for Java
- Test Runner for Java
- Spring Boot Extension Pack
- Spring Boot Tools
- Spring Boot Dashboard
- Spring Initializr Java Support
- Docker
- Container Tools
- GitLens
- Prettier
- ESLint

### Verification

    java -version
    mvn -version
    $env:JAVA_HOME
    git --version
    docker --version
    docker compose version

### Skipped

    .vscode/settings.json
    .vscode/extensions.json

### Why

Prepared VS Code as the primary development environment without adding unnecessary workspace-specific configuration.

---

## B0.4 — Create Spring Boot Project Structure

**Status:** ✅ Completed

Created the backend repository structure.

    backend/
    ├── alumni-service/
    ├── api-gateway/
    ├── auth-service/
    ├── community-service/
    ├── docs/
    ├── event-service/
    ├── jnv-service/
    ├── mentorship-service/
    ├── notification-service/
    ├── opportunity-service/
    ├── user-service/
    ├── .gitignore
    ├── pom.xml
    └── README.md

Created the root Maven project with `pom` packaging.

### Why

Established the multi-module backend foundation before creating individual Spring Boot services.

---

## B0.5 — Configure Maven

**Status:** ✅ Completed

Configured the root Maven `pom.xml`.

### Configuration

- Group ID: `com.we-are-navodayan`
- Artifact ID: `we-are-navodayan-backend`
- Version: `0.0.1-SNAPSHOT`
- Packaging: `pom`
- Java: `21`
- Maven Compiler Release: `21`
- Maven Compiler Plugin: `3.14.1`

### Compiler Configuration

    <maven.compiler.release>21</maven.compiler.release>

### Verification

    mvn help:effective-pom -N

### Result

    BUILD SUCCESS

Effective POM confirmed Java 21 and compiler release 21.

---

## B0.6 — Configure Git Workflow

**Status:** ✅ Completed

Initialized Git and configured `main` as the primary branch.

### Commands

    git init
    git branch -M main

Configured Git identity:

    git config user.name "Sanjay Kumar"
    git config user.email "ersanjay426@gmail.com"

Added files:

    git add .

Created Phase 0 commit:

    git commit -m "Phase 0 : Project & Development Setup"

Commit:

    013312d

Configured GitHub remote:

    git remote add origin https://github.com/sanjay-dynasty/we-are-navodayan-backend.git

Pushed:

    git push -u origin main

### Result

    main → origin/main

---

## B0.7 — Configure Environment Profiles

**Status:** ⏸️ Deferred

Environment profile handling was initially planned as a separate Phase 0 activity.

The actual profile configuration was implemented during **B1.5 — Configuration Management**, where the services received:

    local
    dev
    staging
    prod

No separate implementation was required in Phase 0.

---

## B0.8 — Create Initial Service Template

**Status:** ✅ Completed as part of Phase 1

The individual Spring Boot service templates were created and configured during **B1.3 — Configure Spring Boot Services**.

The implementation was grouped with the Microservices Foundation because the service templates depend on the finalized service boundaries and common structure.

---

# Phase 0 Overall

Completed the backend development foundation:

- Defined microservice architecture
- Defined initial service boundaries
- Installed Java 21
- Installed Maven
- Installed Git
- Configured VS Code
- Installed Docker and Docker Compose
- Configured WSL 2 and Ubuntu
- Created backend repository structure
- Created root Maven project
- Configured Maven compiler
- Initialized Git
- Configured `main` branch
- Created initial commit
- Connected GitHub repository
- Pushed `main` branch

## Phase 0 Final Checklist

| Item | Status |
|---|---|
| Java 21 LTS | ✅ |
| JAVA_HOME | ✅ |
| Maven 3.9.16 | ✅ |
| MAVEN_HOME | ✅ |
| Git | ✅ |
| VS Code | ✅ |
| Docker | ✅ |
| Docker Compose | ✅ |
| WSL 2 | ✅ |
| Ubuntu | ✅ |
| Docker WSL Integration | ✅ |
| Docker Engine | ✅ |
| Docker Hello World | ✅ |
| Backend Structure | ✅ |
| Root Maven POM | ✅ |
| Maven Effective POM | ✅ |
| Git Repository | ✅ |
| Main Branch | ✅ |
| Initial Commit | ✅ |
| GitHub Remote | ✅ |
| GitHub Push | ✅ |

## Phase 0 Status

**Completed**

## Phase 0 Commit

    git commit -m "Phase 0 : Project & Development Setup"

Commit:

    013312d

# Phase 1 — Microservices Foundation

## B1.1 — Define Service Boundaries

**Status:** ✅ Completed

Defined the backend microservice boundaries and responsibilities for the We Are Navodayan platform.

### Services

| Service | Responsibility |
|---|---|
| `api-gateway` | External entry point, routing, filters, CORS and rate limiting |
| `auth-service` | Registration, login, JWT and refresh token management |
| `user-service` | User profiles, JNV/batch, profession, location, skills and interests |
| `jnv-service` | JNV directory, school information and metadata |
| `alumni-service` | Alumni information and discovery |
| `community-service` | Posts, comments, likes and feeds |
| `opportunity-service` | Jobs, internships, scholarships and opportunities |
| `mentorship-service` | Mentors, mentees and mentorship relationships |
| `event-service` | Events, registrations and meetups |
| `notification-service` | Notification creation and delivery |

### Architecture Decisions

- Each service owns its domain data.
- No direct database access between services.
- Services are independently deployable and scalable.
- REST is used for synchronous communication.
- Kafka/event-driven communication is deferred until required by an actual business workflow.
- Common base package:

    com.wearenavodayan

### Why

Clear service boundaries reduce coupling and allow individual services to evolve, deploy and scale independently.

---

## B1.2 — Create Common Service Structure

**Status:** ✅ Completed

Created the common project structure for all business microservices.

### Business Services

    auth-service
    user-service
    jnv-service
    alumni-service
    community-service
    opportunity-service
    mentorship-service
    event-service
    notification-service

### Common Java Packages

    controller
    service
    repository
    entity
    dto
    mapper
    exception
    config

### DTO Structure

    dto/
    ├── request/
    └── response/

### Exception Structure

    exception/
    ├── handler/
    └── model/

### Gateway Structure

    api-gateway/
    └── src/main/java/com/wearenavodayan/apigateway/
        ├── config/
        ├── filter/
        └── exception/

### Why

Created a consistent structure across services so future development follows the same architectural pattern.

---

## B1.3 — Configure Spring Boot Services

**Status:** ✅ Completed

Created and configured all required Spring Boot services.

### Configuration

- Java 21
- Spring Boot 4.1.1
- Maven
- Spring Cloud Gateway for API Gateway
- Individual service ports
- Basic application structure
- Initial test setup

### Service Ports

| Service | Port |
|---|---:|
| API Gateway | 8080 |
| Auth Service | 8081 |
| User Service | 8082 |
| JNV Service | 8083 |
| Alumni Service | 8084 |
| Community Service | 8085 |
| Opportunity Service | 8086 |
| Mentorship Service | 8087 |
| Event Service | 8088 |
| Notification Service | 8089 |

### Verification

    mvn clean verify

### Result

All services compiled successfully and their initial tests passed.

### Why

Established independently runnable Spring Boot services before implementing business functionality.

---

## B1.4 — Configure Common Dependencies

**Status:** ✅ Completed

Configured common dependencies required for the initial service foundation.

### Added

- Spring Web MVC
- Spring Boot Actuator
- Spring Boot testing dependencies

### Deferred

Validation dependency was not added globally because validation will be introduced when DTO/API validation is actually required.

### Why

Avoided unnecessary dependencies and kept each service focused on its current requirements.

---

## B1.5 — Configure Configuration Management

**Status:** ✅ Completed

Configured service-level application properties and environment profiles.

### Service Configuration

Each service was configured with:

    spring.application.name=<service-name>
    server.port=<service-port>
    spring.profiles.default=local

### Environment Profiles

    local
    dev
    staging
    prod

Created:

    application-local.properties
    application-dev.properties
    application-staging.properties
    application-prod.properties

### Configuration Principles

- Service-specific configuration
- Environment-specific configuration
- Local profile as default development profile
- No hardcoded secrets
- Configuration separated from business logic

### Verification

    mvn clean verify

### Result

Complete multi-module Maven build passed successfully.

### Why

Prepared the services for different deployment environments without modifying application code.

---

## B1.6 — Configure Logging

**Status:** ✅ Completed

Configured standardized logging across all business services.

### Added

    logback-spring.xml

to all business services.

### Log Information

Configured logs to include:

- Timestamp
- Log level
- Service name
- Profile
- Thread
- Logger
- Message

### Example

    2026-09-17T15:22:31.691+05:30 INFO
    [auth-service] [default] [main]
    ...

### Local Logging

Configured DEBUG logging for:

    com.wearenavodayan

in the local environment.

### Verification

Started `auth-service` and verified standardized startup logs.

### Why

Provides consistent service-level logs and prepares the platform for centralized observability in later infrastructure phases.

---

## B1.7 — Configure Health Checks

**Status:** ✅ Completed

Configured Spring Boot Actuator health monitoring.

### Endpoints

    /actuator/health
    /actuator/info

Enabled:

- Liveness
- Readiness

### Verification

Started:

    auth-service :8081

Verified:

    /actuator/health

### Example Response

    {
      "groups": [
        "liveness",
        "readiness"
      ],
      "status": "UP"
    }

### Why

Health endpoints will later support:

- Container health checks
- Load balancers
- ECS deployments
- Monitoring
- Deployment verification

---

## B1.8 — Configure API Standards

**Status:** ✅ Completed

Established common REST API conventions across business services.

### API Versioning

    /api/v1

### HTTP Methods

| Method | Purpose |
|---|---|
| POST | Create |
| GET | Read |
| PUT | Full Update |
| PATCH | Partial Update |
| DELETE | Delete |

### Standard Status Codes

Defined conventions for:

    200
    201
    204
    400
    401
    403
    404
    409
    422
    429
    500
    503

### DTO Structure

    dto/
    ├── request/
    └── response/

### Standard Success Response

    public record ApiResponse<T>(
            boolean success,
            T data,
            String message
    ) {
    }

### Example

    {
      "success": true,
      "data": {},
      "message": "Operation successful"
    }

### Standard Error Response

    public record ApiErrorResponse(
            boolean success,
            String code,
            String message,
            Instant timestamp,
            String path
    ) {
    }

### Example

    {
      "success": false,
      "code": "RESOURCE_NOT_FOUND",
      "message": "Resource not found",
      "timestamp": "2026-09-17T16:00:00Z",
      "path": "/api/v1/users/123"
    }

### Additional Standards

- REST resources use plural nouns.
- Kebab-case is used where appropriate.
- Pagination parameters:

    page
    size
    sort

- OpenAPI/Swagger documentation conventions established for future implementation.

### Why

Ensures consistent API contracts across all microservices.

---

## B1.9 — Configure Inter-Service Communication

**Status:** ✅ Completed

Established the initial synchronous REST communication foundation between microservices.

### Communication Architecture

    Client
      ↓
    API Gateway
      ↓
    Microservice
      ↓
    REST
      ↓
    Another Microservice

---

### B1.9.1 — Define Communication Strategy

**Status:** ✅ Completed

Defined:

- REST for synchronous communication.
- No direct cross-service database access.
- Service URLs are configuration-driven.
- Asynchronous messaging will be introduced when required by a real business workflow.

---

### B1.9.2 — REST Client Foundation

**Status:** ✅ Completed

Configured Spring `RestClient` in `user-service`.

Created:

    user-service/
    └── src/main/java/com/wearenavodayan/userservice/
        └── config/
            └── RestClientConfig.java

### Configuration

- Java `HttpClient`
- Connection timeout
- Read timeout
- Spring `RestClient`

### Timeouts

    Connection timeout: 3 seconds
    Read timeout: 5 seconds

### Why

Prevents downstream service calls from blocking indefinitely.

---

### B1.9.3 — Configure Service URLs

**Status:** ✅ Completed

Configured the JNV service base URL in the user service local profile.

    services.jnv.base-url=http://localhost:8083

### Why

Keeps service endpoints configurable and avoids embedding environment-specific URLs into Java code.

---

### B1.9.4 — Create Service-to-Service REST Client

**Status:** ✅ Completed

Created:

    user-service/
    └── src/main/java/com/wearenavodayan/userservice/
        └── client/
            └── JnvServiceClient.java

Implemented:

    GET /api/v1/jnvs/{jnvId}

### Communication

    User Service
         |
         | REST
         ↓
    JNV Service

### Why

Established a reusable pattern for synchronous communication between microservices.

---

### B1.9.5 — Configure REST Timeouts

**Status:** ✅ Completed

Configured:

    Connect timeout: 3 seconds
    Read timeout: 5 seconds

Implemented using Java `HttpClient` and Spring's `JdkClientHttpRequestFactory`.

### Why

Protects the calling service from slow or unavailable downstream services.

---

### B1.9.6 — Basic REST Error Handling

**Status:** ✅ Completed

Created:

    user-service/
    └── src/main/java/com/wearenavodayan/userservice/
        └── exception/
            └── JnvServiceClientException.java

The JNV REST client handles:

- `4xx` client errors
- `5xx` server errors
- Connection failures
- Timeout-related REST client failures

### Error Flow

    JNV Service
         |
         +---- 4xx ----------------┐
         |                         |
         +---- 5xx ----------------┤
         |                         ↓
         +---- Connection Error --> JnvServiceClientException
         |
         +---- Timeout ------------┘

### Why

Provides a consistent application-level exception instead of exposing low-level REST client exceptions throughout the service.

---

### B1.9.7 — Add Kafka Dependency

**Status:** ⏸️ Deferred**

Kafka was intentionally not added during Phase 1.

### Reason

Kafka will be introduced when an actual asynchronous business workflow requires it.

Potential future use cases:

    User Registration
          ↓
    User Created Event
          ↓
    Notification Service

or:

    Opportunity Application
          ↓
    Application Created Event
          ↓
    Notification / Analytics

### Decision

Do not add Kafka infrastructure merely for the sake of completing the architecture checklist.

---

### B1.9.8 — Kafka Producer/Consumer Foundation

**Status:** ⏸️ Deferred**

No Kafka producer/consumer configuration was created during Phase 1.

Kafka will be implemented together with the first real event-driven business workflow.

---

### B1.9.9 — Domain Event Convention

**Status:** ⏸️ Deferred**

Domain event contracts were not implemented during Phase 1.

Event structure and topic conventions will be defined when the first asynchronous business workflow is implemented.

---

### B1.9.10 — Verify Inter-Service Communication

**Status:** ✅ Completed

Verified the complete backend after implementing the REST communication foundation.

### Verification

    mvn clean verify

---

# Phase 1 Overall

Established the complete initial microservices foundation:

- Defined microservice boundaries and responsibilities
- Created common service structures
- Configured Spring Boot services
- Assigned individual service ports
- Added common dependencies
- Configured environment profiles
- Configured standardized logging
- Added Actuator health checks
- Established REST API standards
- Established API versioning
- Defined standard HTTP status codes
- Defined standard success and error responses
- Established synchronous REST communication
- Configured `RestClient`
- Configured service URLs
- Created JNV service REST client
- Configured connection and read timeouts
- Added basic REST error handling
- Intentionally deferred Kafka until an actual asynchronous business requirement exists

## Phase 1 Final Checklist

| Item | Status |
|---|---|
| Service Boundaries | ✅ |
| Common Service Structure | ✅ |
| Spring Boot Services | ✅ |
| Service Ports | ✅ |
| Common Dependencies | ✅ |
| Configuration Management | ✅ |
| Environment Profiles | ✅ |
| Logging | ✅ |
| Health Checks | ✅ |
| API Standards | ✅ |
| API Versioning | ✅ |
| Standard HTTP Status Codes | ✅ |
| Standard Success Response | ✅ |
| Standard Error Response | ✅ |
| Inter-Service Communication Strategy | ✅ |
| REST Client Foundation | ✅ |
| Service URL Configuration | ✅ |
| JNV REST Client | ✅ |
| REST Timeouts | ✅ |
| REST Error Handling | ✅ |
| Kafka Dependency | ⏸️ Deferred |
| Kafka Producer/Consumer | ⏸️ Deferred |
| Domain Event Convention | ⏸️ Deferred |
| Inter-Service Communication Verification | ✅ |

## Phase 1 Status

**Completed**

## Phase 1 Architectural Decision

Kafka has intentionally been deferred until the platform has a real asynchronous business workflow that requires event-driven communication.