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

# Phase 2 — Database Foundation

**Project:** We Are Navodayan  
**Technology Stack:** Java 21, Spring Boot 4.1.1, Spring Data JPA, Hibernate, PostgreSQL 17, Flyway, HikariCP, Maven, JUnit 5  
**Status:** Core foundation completed; entity, migration, transaction, pooling and integration-test implementation currently covers `user-service` and `jnv-service`.

---

## Phase 2 Overview

Phase 2 establishes the database foundation for the We Are Navodayan microservices platform. It defines service-level database ownership, configures PostgreSQL, introduces JPA entities and repositories, manages database schema changes with Flyway, adds indexes, implements service-layer transaction management, configures connection pools, and verifies database functionality through automated tests.

### Objectives

- Establish independent database ownership for business microservices.
- Configure PostgreSQL for local development.
- Integrate Spring Data JPA and Hibernate.
- Create domain entities and repositories.
- Manage schema changes through Flyway migrations.
- Add database indexes and uniqueness constraints.
- Configure transactional service-layer operations.
- Configure HikariCP connection pools.
- Test persistence, constraints, and service behavior.
- Verify the complete Maven multi-module project.

### Phase Checklist

| Task | Description | Status |
|---|---|---|
| B2.1 | Design Service Data Ownership | Completed |
| B2.2 | Configure PostgreSQL | Completed |
| B2.3 | Configure Spring Data JPA | Foundation configured; entity/repository implementation started |
| B2.4 | Define Entities & Relationships | Implemented for User and JNV domains |
| B2.5 | Configure Database Migrations | Flyway migrations implemented for User and JNV domains |
| B2.6 | Configure Indexes | Implemented in the relevant migrations |
| B2.7 | Configure Transactions | Implemented and tested in User and JNV services |
| B2.8 | Configure Connection Pooling | HikariCP configured for User and JNV services |
| B2.9 | Database Testing | Integration tests implemented; full Maven verification passed |

---

## B2.1 — Design Service Data Ownership

**Status:** Completed

### Objective

Define which microservice owns each domain's data and prevent services from directly accessing databases owned by other services.

### Database Ownership

Each business microservice has its own logical PostgreSQL database.

| Microservice | Database |
|---|---|
| `auth-service` | `auth_db` |
| `user-service` | `user_db` |
| `jnv-service` | `jnv_db` |
| `alumni-service` | `alumni_db` |
| `community-service` | `community_db` |
| `opportunity-service` | `opportunity_db` |
| `mentorship-service` | `mentorship_db` |
| `event-service` | `event_db` |
| `notification-service` | `notification_db` |
| `api-gateway` | No business database |

### Architecture Decisions

- Each business microservice owns its domain data.
- A service must not directly query another service's database.
- Cross-service data access uses service APIs or a deliberately designed asynchronous workflow.
- Database relationships are maintained within the owning service.
- Cross-service foreign-key relationships are avoided.
- PostgreSQL is the primary relational database.
- Redis is reserved for appropriate future caching and other use cases.

### Result

The database ownership model establishes clear boundaries for persistence, migrations, transactions, and independent service evolution.

---

## B2.2 — Configure PostgreSQL

**Status:** Completed

### Objective

Configure a local PostgreSQL environment and connect the Spring Boot services to their designated databases.

### PostgreSQL Environment

| Setting | Value |
|---|---|
| Docker container | `we-are-navodayan-postgres` |
| Docker image | `postgres:17` |
| Host port | `5432` |
| Database user | `navodayan` |
| Default database | `postgres` |
| Password source | `DB_PASSWORD` environment variable |

PostgreSQL runs locally using Docker. The database password is supplied through an environment variable instead of being embedded in application code.

### Databases Created

- `auth_db`
- `user_db`
- `jnv_db`
- `alumni_db`
- `community_db`
- `opportunity_db`
- `mentorship_db`
- `event_db`
- `notification_db`

These databases establish the intended ownership model. A database existing does not mean its complete domain schema and business functionality have already been implemented.

### Spring Boot Configuration

Local PostgreSQL connection settings were configured in the service application properties.

Example:

```properties
spring.config.activate.on-profile=local

spring.datasource.url=jdbc:postgresql://localhost:5432/auth_db
spring.datasource.username=navodayan
spring.datasource.password=${DB_PASSWORD}

spring.jpa.hibernate.ddl-auto=validate
spring.jpa.open-in-view=false
spring.jpa.show-sql=false
spring.jpa.properties.hibernate.format_sql=true
spring.jpa.properties.hibernate.jdbc.time_zone=UTC
```

**Important:** The database name must match the database owned by the specific service. The example above is for `auth-service`; the User and JNV services use their own databases.

### Configuration Decisions

- Use environment variables for database credentials.
- Keep local database settings in the local profile.
- Use Hibernate schema validation rather than automatic schema creation or modification.
- Disable Open EntityManager in View.
- Avoid enabling SQL logging by default.
- Use UTC for Hibernate JDBC timestamp handling.

### Result

PostgreSQL connectivity was established for the business services, and the database environment was available for migration execution and integration testing.

---

## B2.3 — Configure Spring Data JPA

**Status:** Foundation configured; implementation started for User and JNV domains

### Objective

Integrate Spring Data JPA and Hibernate to provide object-relational mapping and repository-based database operations.

### Technology Responsibilities

- **Spring Data JPA:** Provides repository abstractions and CRUD operations.
- **Hibernate:** Implements JPA object-relational mapping.
- **PostgreSQL driver:** Connects the application to PostgreSQL.
- **Flyway:** Manages version-controlled database schema changes.

### Repository Pattern

The intended persistence flow is:

```text
Service Layer
     |
     v
Spring Data JPA Repository
     |
     v
Hibernate / JPA
     |
     v
PostgreSQL Database
```

### Implemented Repositories

The following repositories were implemented for the current domain models:

- `JnvRepository`
- `UserProfileRepository`

They provide standard persistence operations and domain-specific queries, including lookups by school code, authentication user ID, and JNV ID.

### Schema Management

Hibernate is configured to validate the entity mappings against the database schema. Flyway is responsible for applying schema migrations.

This separates application persistence mappings from database schema evolution.

### Result

The persistence foundation is implemented and verified for the User and JNV domains. Complete domain entities and repositories for the remaining microservices are future work.

---

## B2.4 — Define Entities & Relationships

**Status:** Completed for User and JNV domains

### Objective

Represent the core User and JNV domain data as JPA entities and map those entities to PostgreSQL tables.

### 1. JNV Entity

**Class:** `Jnv`

**Service:** `jnv-service`

**Database:** `jnv_db`

The entity represents a Jawahar Navodaya Vidyalaya record.

| Field | Purpose |
|---|---|
| `id` | Entity identifier |
| `schoolCode` | School code with uniqueness enforcement |
| `schoolName` | School name |
| `state` | State |
| `district` | District |
| `address` | School address |
| `pinCode` | Postal PIN code |
| `active` | Indicates whether the JNV record is active |

The entity is persisted through `JnvRepository`.

### 2. User Profile Entity

**Class:** `UserProfile`

**Service:** `user-service`

**Database:** `user_db`

The entity represents a user's platform profile.

| Field | Purpose |
|---|---|
| `id` | Entity identifier |
| `authUserId` | Identifier associated with the authentication user; uniqueness is enforced |
| `fullName` | User's full name |
| `bio` | Profile biography |
| `batchYear` | Navodaya batch year |
| `jnvId` | Identifier of the associated JNV |
| `profileImageUrl` | Profile image location or URL |

The entity is persisted through `UserProfileRepository`.

### Relationship Design

The profile stores its JNV association as an identifier. The JNV and User Profile domains belong to different services and different databases.

Consequently, the User Service must not establish a cross-database JPA relationship that directly queries the JNV database. Cross-service verification or retrieval must use the established service communication layer.

The User Service already has a REST client foundation for communicating with the JNV Service.

### Result

The initial domain persistence models are in place for JNV records and user profiles. The remaining business domains will receive their own entities and relationships as their features are implemented.

---

## B2.5 — Configure Database Migrations

**Status:** Completed for User and JNV domains

### Objective

Manage database schema changes in a repeatable, version-controlled manner.

### Technology

Flyway database migrations.

### Implemented Approach

- Store migration scripts with their owning service.
- Use versioned migration files.
- Let Flyway validate and apply migrations during application startup.
- Keep entity mappings aligned with the migrated database schema.
- Use Hibernate validation to detect schema mismatches.

### Migration Verification

During application startup, Flyway validates previously applied migrations and checks whether the database schema is up to date.

The User Service startup logs confirmed that two migrations were validated and the schema was already at version 2, with no additional migration required during that run.

The JNV and User services have migration-managed schemas for their implemented entities.

### Why Flyway?

- Schema changes are version-controlled.
- Database initialization is repeatable.
- Existing environments can be migrated incrementally.
- Schema history is tracked in the database.
- Hibernate is not responsible for silently modifying production schemas.

### Result

Flyway migration execution and schema validation were verified for the implemented User and JNV database schemas.

---

## B2.6 — Configure Indexes

**Status:** Completed for the implemented User and JNV schemas

### Objective

Improve lookup performance and enforce important data-integrity rules through database indexes and uniqueness constraints.

### Implemented Indexing Areas

The migrations define indexes and uniqueness rules appropriate to the implemented domain models.

Important lookup fields include:

- JNV school code.
- User authentication user ID.
- User profile JNV association.

### Uniqueness Rules

| Domain | Field | Purpose |
|---|---|---|
| JNV | `schoolCode` | Prevent duplicate school codes |
| User Profile | `authUserId` | Prevent multiple profiles from using the same authentication user ID |

Database-level uniqueness is important because application-level checks alone cannot prevent concurrent requests from creating duplicate records.

### Verification

Integration tests attempted duplicate inserts for both domains and verified that the database rejected them.

The expected database constraint violations in these negative tests do not indicate a failed test suite.

### Result

The implemented schemas include indexing and uniqueness protections for the principal lookup and identity fields. Indexing for future search and filtering features will be introduced as those access patterns are defined.

---

## B2.7 — Configure Transactions

**Status:** Completed and tested for User and JNV services

### Objective

Establish service-layer transaction boundaries so that database operations execute with the intended transactional behavior.

### Implemented Classes

**JNV Service**

`jnv-service/src/main/java/com/wearenavodayan/jnvservice/service/JnvService.java`

**User Profile Service**

`user-service/src/main/java/com/wearenavodayan/userservice/service/UserProfileService.java`

### Transaction Strategy

Both services use class-level read-only transaction configuration:

```java
@Service
@Transactional(readOnly = true)
public class ExampleService {
    // Read operations
}
```

Write operations explicitly override the read-only default:

```java
@Transactional
public ExampleEntity create(ExampleEntity entity) {
    return repository.save(entity);
}
```

### Implemented Operations

Both services implement the appropriate methods for:

- Creating records.
- Retrieving records by ID.
- Retrieving records using domain-specific identifiers.
- Listing records.
- Updating existing records.
- Deleting records.
- Checking whether records exist.

The JNV Service supports lookup by school code. The User Service supports lookup by authentication user ID and retrieval by JNV ID.

Missing records are handled using `EntityNotFoundException`.

### Transaction Tests

Dedicated test classes were created:

- `JnvServiceTransactionTests`
- `UserProfileTransactionTests`

The tests verify service behavior and inspect transaction metadata to confirm the intended read-only and write transaction configuration.

The transaction test classes contain three tests each, and both suites passed.

### Important Boundary

Transaction management is currently implemented for the User and JNV services. The current tests verify transaction configuration and CRUD behavior; they do not constitute a complete rollback test for a multi-step business transaction.

### Result

Service-layer transaction boundaries are established for the two implemented domain services, ready for later controller and business workflow integration.

---

## B2.8 — Configure Connection Pooling

**Status:** Completed for User and JNV services

### Objective

Configure database connection pooling to reuse database connections efficiently and limit the number of concurrent connections opened by each service.

### Technology

HikariCP, the JDBC connection pool used by the Spring Boot datasource configuration.

### Configuration

The following settings were added to the local profiles.

For `jnv-service`:

```properties
spring.datasource.hikari.pool-name=JnvServiceHikariPool
spring.datasource.hikari.maximum-pool-size=5
spring.datasource.hikari.minimum-idle=1
spring.datasource.hikari.connection-timeout=30000
spring.datasource.hikari.idle-timeout=600000
spring.datasource.hikari.max-lifetime=1800000
```

For `user-service`, the same pool sizing and timeout values are used, with the pool name:

```properties
spring.datasource.hikari.pool-name=UserServiceHikariPool
```

### Configuration Explanation

| Property | Value | Purpose |
|---|---:|---|
| `pool-name` | Service-specific | Makes connection pool logs identifiable |
| `maximum-pool-size` | `5` | Limits the pool to five connections |
| `minimum-idle` | `1` | Targets at least one idle connection |
| `connection-timeout` | `30000` ms | Maximum wait for a connection |
| `idle-timeout` | `600000` ms | Idle connection timeout |
| `max-lifetime` | `1800000` ms | Maximum connection lifetime |

These are local development settings, not final production capacity decisions. Production values should be sized against expected traffic, database connection limits, service replica counts, and workload characteristics.

### Verification

The services started successfully and established PostgreSQL connections. The full Maven verification also passed after these changes.

### Result

Explicit HikariCP pool configuration is in place for the User and JNV services. Other services may still use their default pool configuration until their database workloads are implemented and tuned.

---

## B2.9 — Database Testing

**Status:** Completed for the current database foundation

### Objective

Verify database connectivity, schema validation, migrations, entity persistence, repository queries, uniqueness constraints, and service-layer behavior through automated tests.

### Test Infrastructure

- JUnit 5.
- Spring Boot test support.
- Spring application context tests.
- Spring Data JPA repositories.
- PostgreSQL local development database.
- Flyway migration validation.
- Maven multi-module build verification.

### User Service Integration Tests

**Test class:** `UserServiceApplicationTests`

The expanded suite covers:

1. Application context loading.
2. Saving and retrieving a user profile.
3. Finding a profile by authentication user ID.
4. Checking whether a profile exists for an authentication user ID.
5. Retrieving profiles by JNV ID.
6. Rejecting duplicate authentication user IDs.

### JNV Service Integration Tests

**Test class:** `JnvServiceApplicationTests`

The expanded suite covers:

1. Application context loading.
2. Saving and retrieving a JNV record.
3. Finding a JNV by school code.
4. Checking whether a school code exists.
5. Rejecting duplicate school codes.

### Service Transaction Tests

| Test Class | Tests |
|---|---:|
| `JnvServiceTransactionTests` | 3 |
| `UserProfileTransactionTests` | 3 |

These tests cover CRUD service behavior, missing-record handling, and transaction metadata.

### Test Cleanup

The integration tests clean up records created during testing to reduce interference between test executions.

### Timezone Configuration

The full verification run used the following PowerShell session settings:

```powershell
$env:DB_PASSWORD="navodayan_local"
$env:JAVA_TOOL_OPTIONS="-Duser.timezone=UTC"
```

The timezone setting was applied to the current shell session for consistent test execution; it was not intended as a permanent operating-system setting.

### Targeted Transaction Test Command

```powershell
mvn -pl jnv-service,user-service "-Dtest=JnvServiceTransactionTests,UserProfileTransactionTests" test
```

**Result:** Both services passed their targeted transaction test suites.

### Full Build Verification

Command executed:

```powershell
mvn clean verify
```

The command completed with `BUILD SUCCESS`, and all 11 Maven reactor modules reported success.

### Result

The database foundation passed targeted transaction testing and the full multi-module Maven verification.

---

## Phase 2 — Final Architecture

```text
We Are Navodayan
       |
       v
Spring Boot Microservices
       |
       +------------------------+
       |                        |
       v                        v
  User Service             JNV Service
       |                        |
       v                        v
 UserProfileService        JnvService
       |                        |
       v                        v
 UserProfileRepository     JnvRepository
       |                        |
       v                        v
 Hibernate / JPA           Hibernate / JPA
       |                        |
       v                        v
 HikariCP Pool              HikariCP Pool
       |                        |
       v                        v
 PostgreSQL                 PostgreSQL
    user_db                    jnv_db
       |                        |
       v                        v
 Flyway Migrations          Flyway Migrations
```

Each service accesses its own database. Cross-service communication remains API-based rather than direct database access.

---

## Phase 2 — Final Checklist

| Item | Status |
|---|---|
| Database ownership boundaries defined | Completed |
| PostgreSQL configured through Docker | Completed |
| Separate logical databases created | Completed |
| Database credentials externalized | Completed |
| JPA/Hibernate persistence foundation | Completed |
| JNV entity and repository | Implemented |
| User Profile entity and repository | Implemented |
| Flyway migrations for JNV and User | Implemented |
| Hibernate schema validation | Configured |
| Database indexes and uniqueness rules | Implemented for current schemas |
| Service-layer transaction management | Implemented for JNV and User |
| Transaction behavior tests | Passed |
| HikariCP explicit configuration | Implemented for JNV and User |
| JNV database integration tests | Passed |
| User database integration tests | Passed |
| Full Maven verification | Passed |
| All business schemas and entities implemented | Not yet complete |

---

## Git History

The following commits are recorded in the backend repository:

| Commit | Description |
|---|---|
| `5989511` | Phase 2.1–2.2: Design and Configure PostgreSQL |
| `d4c6422` | Phase 2.2: Stabilize PostgreSQL Test Configuration |
| `ef2bae8` | Phase 2.4–2.6: Add JPA Entities, Flyway Migrations and Indexes |
| `b5a049a` | Phase 2.7: Add Service-Layer Transaction Management |
| `b66057d` | Phase 2.8–2.9: Configure HikariCP and Add Database Integration Tests |

The current backend repository was confirmed clean and synchronized with `origin/main` after these commits.

---

## Outstanding Work After Phase 2

The database foundation is complete for the currently implemented User and JNV domains, but the following work remains for the overall platform:

- Complete entity and repository implementations for the remaining business domains.
- Add domain-specific migrations, constraints, and indexes as those schemas are introduced.
- Add persistence and integration tests for each newly implemented service.
- Add REST controllers and DTOs so database-backed functionality is exposed through APIs.
- Introduce production-specific connection pool sizing and managed database credentials during deployment preparation.
- Add explicit rollback tests when multi-operation transactional business workflows are implemented.

## Phase 2 Conclusion

Phase 2 established the PostgreSQL and JPA foundation, Flyway migration strategy, database constraints, service-layer transaction configuration, connection pooling, and automated persistence tests. The User and JNV services are the first implemented database-backed domains, and the complete Maven multi-module verification passed.

**Next planned milestone:** Phase 3 — API Gateway & Service Discovery, beginning with an inspection of the existing gateway configuration before implementing any missing functionality.