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

# Phase 3 — API Gateway & Service Discovery

**Project:** We Are Navodayan

**Technology Stack:** Java 21, Spring Boot 4.1.1, Spring Cloud Gateway Server WebMVC, Spring Boot Actuator, Spring MVC, Maven, JUnit 5, Mockito

**Status:** Phase 3.1–3.8 implementation completed; targeted API Gateway tests passed. Advanced integration testing of downstream failures, timeouts, and exception handling remains outstanding.

---

## Phase 3 Overview

Phase 3 establishes the API Gateway as the central entry point for the We Are Navodayan microservices platform. It configures request routing, request filtering, cross-origin resource sharing (CORS), rate limiting, downstream service communication settings, API versioning, correlation IDs, and standardized gateway error responses.

The gateway runs on port `8080` and routes requests to the appropriate backend microservices.

### Objectives

- Configure the API Gateway.
- Route requests to the appropriate microservices.
- Add request filtering and correlation IDs.
- Configure CORS for frontend integration.
- Implement request rate limiting.
- Configure downstream service URLs and HTTP client timeouts.
- Introduce centralized API versioning.
- Standardize gateway error responses.
- Verify gateway configuration and behavior through automated tests.

### Phase Checklist

| Task | Description | Status |
|---|---|---|
| 3.1 | Configure API Gateway | Completed |
| 3.2 | Configure Routing | Completed |
| 3.3 | Configure Request Filtering | Completed |
| 3.4 | Configure CORS | Completed |
| 3.5 | Configure Rate Limiting | Completed |
| 3.6 | Configure Service Communication | Configuration completed; actual timeout behavior needs integration testing |
| 3.7 | Configure API Versioning | Completed |
| 3.8 | Gateway Error Handling | Implementation completed; additional integration testing remains |

---

## 3.1 — Configure API Gateway

**Status:** Completed

### Objective

Establish a centralized entry point through which frontend applications access backend microservices.

### Technology

- Spring Boot 4.1.1
- Spring Cloud Gateway Server WebMVC
- Spring Boot Actuator
- Spring MVC

### Configuration

**File:** `api-gateway/src/main/resources/application.properties`

The gateway is configured with the following properties:

```properties
spring.application.name=api-gateway
spring.profiles.default=local
server.port=8080

management.endpoints.web.exposure.include=health,info,gateway
management.endpoint.health.show-details=never
management.endpoint.gateway.access=read-only

management.endpoint.health.probes.enabled=true
management.health.livenessstate.enabled=true
management.health.readinessstate.enabled=true

management.info.env.enabled=true
info.app.name=We Are Navodayan API Gateway
info.app.description=Central entry point for We Are Navodayan microservices
info.app.version=0.0.1-SNAPSHOT
```

### Health Monitoring

Spring Boot Actuator provides health and application information endpoints.

- Health endpoint: `/actuator/health`
- Application information: `/actuator/info`
- Gateway actuator endpoint: `/actuator/gateway`

Only the configured actuator endpoints are exposed through the web management interface.

### Result

The API Gateway configuration establishes the centralized entry point and provides basic health monitoring and application metadata.

---

## 3.2 — Configure Routing

**Status:** Completed

### Objective

Forward incoming API requests to the appropriate downstream microservice based on their URL paths.

### Downstream Service Configuration

The gateway uses configurable base URLs for its services:

```properties
services.auth.base-url=http://localhost:8081
services.user.base-url=http://localhost:8082
services.jnv.base-url=http://localhost:8083
```

### Configured Routes

| Route ID | Request Path | Destination |
|---|---|---|
| `auth-service-route` | `/api/v1/auth/**` | Auth Service, port 8081 |
| `user-service-route` | `/api/v1/users/**` | User Service, port 8082 |
| `jnv-service-route` | `/api/v1/jnvs/**` | JNV Service, port 8083 |

### Route Configuration

```properties
spring.cloud.gateway.server.webmvc.routes[0].id=auth-service-route
spring.cloud.gateway.server.webmvc.routes[0].uri=${services.auth.base-url}
spring.cloud.gateway.server.webmvc.routes[0].predicates[0]=Path=${api.version.base-path}/auth/**

spring.cloud.gateway.server.webmvc.routes[1].id=user-service-route
spring.cloud.gateway.server.webmvc.routes[1].uri=${services.user.base-url}
spring.cloud.gateway.server.webmvc.routes[1].predicates[0]=Path=${api.version.base-path}/users/**

spring.cloud.gateway.server.webmvc.routes[2].id=jnv-service-route
spring.cloud.gateway.server.webmvc.routes[2].uri=${services.jnv.base-url}
spring.cloud.gateway.server.webmvc.routes[2].predicates[0]=Path=${api.version.base-path}/jnvs/**
```

### Routing Behavior

For example, a request to:

`http://localhost:8080/api/v1/users/123`

matches the User Service route and is forwarded to the configured User Service destination.

The gateway configuration does not itself implement the business functionality of the downstream service.

### Result

Three service routes are configured for authentication, user profiles, and JNV directory operations.

---

## 3.3 — Configure Request Filtering

**Status:** Completed

### Objective

Attach a correlation identifier to incoming requests so that a request can be traced across gateway and downstream service logs.

### Implementation

**File:** `api-gateway/src/main/java/com/wearenavodayan/apigateway/filter/CorrelationIdFilter.java`

The filter extends `OncePerRequestFilter` and manages the `X-Correlation-ID` header.

### Implemented Behavior

1. Reads an incoming `X-Correlation-ID` header.
2. Preserves the supplied ID if it matches the permitted format.
3. Generates a UUID if the header is missing.
4. Replaces invalid correlation IDs with a generated UUID.
5. Adds the correlation ID to the response.
6. Wraps the incoming request so the ID can be accessed by downstream processing.

### Validation Rule

The accepted correlation ID format is:

```text
[A-Za-z0-9._-]{1,64}
```

This allows alphanumeric characters, periods, underscores, and hyphens, with a maximum length of 64 characters.

### Tests

Tests cover:

- Preserving a valid incoming correlation ID.
- Generating an ID when the header is missing.
- Replacing an invalid incoming ID.
- Integration with a temporary HTTP server for request processing.

### Result

Correlation IDs provide a consistent identifier for request tracing and troubleshooting.

---

## 3.4 — Configure CORS

**Status:** Completed

### Objective

Allow the local web frontend to communicate with the API Gateway while restricting cross-origin requests to explicitly configured origins, methods, and headers.

### Implementation

**File:** `api-gateway/src/main/java/com/wearenavodayan/apigateway/config/CorsConfig.java`

The configuration implements Spring MVC's `WebMvcConfigurer`.

### CORS Configuration

| Setting | Configured Value |
|---|---|
| Allowed origin | `http://localhost:5173` |
| Allowed methods | GET, POST, PUT, PATCH, DELETE, OPTIONS |
| Allowed headers | Authorization, Content-Type, X-Correlation-ID |
| Exposed response header | X-Correlation-ID |
| Credentials | Disabled |
| Max age | 3600 seconds |

### Explanation

- The configured origin corresponds to the local frontend development server.
- `Authorization` allows clients to send bearer tokens.
- `Content-Type` supports JSON requests.
- `X-Correlation-ID` supports request tracing.
- Exposing `X-Correlation-ID` allows browser clients to read the response header.
- Credentials are disabled in this configuration.

### Tests

`CorsConfigurationTests` inspect the configured CORS mappings, including the allowed origin, methods, headers, exposed headers, credentials, and maximum age.

### Result

The gateway has an explicit local-development CORS policy. Production frontend origins must be configured appropriately before deployment.

---

## 3.5 — Configure Rate Limiting

**Status:** Completed for the in-memory implementation

### Objective

Limit the number of requests accepted from a client during a defined time window to help protect the API Gateway from excessive traffic.

### Implementation

**File:** `api-gateway/src/main/java/com/wearenavodayan/apigateway/filter/RateLimitFilter.java`

The filter uses a concurrent in-memory map keyed by the client's remote IP address.

### Configuration

```properties
gateway.rate-limit.capacity=100
gateway.rate-limit.window-seconds=60
```

### Rate-Limiting Rules

- Maximum configured capacity: 100 requests per client per window.
- Window duration: 60 seconds.
- Rate limiting applies to `/api/` requests.
- OPTIONS requests are excluded.
- Requests exceeding the configured limit receive HTTP `429 Too Many Requests`.
- A cleanup mechanism periodically removes expired rate-limit entries.

### Response Headers

| Header | Purpose |
|---|---|
| `X-RateLimit-Limit` | Configured request limit |
| `X-RateLimit-Remaining` | Remaining requests in the current window |
| `Retry-After` | Indicates how long the client should wait after being limited |

### Important Production Limitation

The implementation uses an in-memory store. Each gateway instance maintains its own counters, so limits are not shared across multiple replicas.

For production deployments with multiple gateway instances, a distributed rate-limiting mechanism, such as Redis-backed counters, should be considered.

The current implementation is a fixed-window rate limiter, not a distributed token-bucket implementation.

### Result

An initial per-client-IP rate limiter is implemented, including response metadata and handling for requests that exceed the configured limit.

---

## 3.6 — Configure Service Communication

**Status:** Configuration completed; actual timeout behavior requires further integration testing

### Objective

Centralize downstream service addresses and configure connection and response-read timeout settings for HTTP communication.

### Service URLs

```properties
services.auth.base-url=http://localhost:8081
services.user.base-url=http://localhost:8082
services.jnv.base-url=http://localhost:8083
```

### HTTP Client Settings

```properties
spring.http.client.connect-timeout=3s
spring.http.client.read-timeout=10s
```

### Explanation

- **Connection timeout:** Configured to 3 seconds for establishing an HTTP connection.
- **Read timeout:** Configured to 10 seconds for reading a response.
- **Centralized service URLs:** Make downstream destinations configurable rather than embedding them in application code.

The gateway uses Spring Cloud Gateway Server WebMVC, which is based on Spring MVC rather than the reactive WebFlux gateway.

### Verification Boundary

Automated tests verified the service URL and timeout property configuration. These tests did not prove that a real downstream connection failure or slow response is terminated at the exact configured duration.

Additional integration tests are required to verify actual timeout behavior.

### Result

Downstream service addresses and HTTP client timeout properties are configured for the gateway.

---

## 3.7 — Configure API Versioning

**Status:** Completed

### Objective

Introduce a centralized API version so future API changes can be managed without scattering version strings throughout the route configuration.

### Configuration

```properties
api.version.current=v1
api.version.base-path=/api/${api.version.current}
```

### Versioned Routes

| API | Versioned Path |
|---|---|
| Authentication | `/api/v1/auth/**` |
| User profiles | `/api/v1/users/**` |
| JNV directory | `/api/v1/jnvs/**` |

### Benefits

- Keeps API versioning consistent across routes.
- Makes the current API version configurable.
- Provides a path-based versioning strategy.
- Establishes a foundation for introducing a future API version.

### Tests

`ApiVersioningConfigurationTests` verify the version properties and the configured versioned route paths.

### Result

The current gateway routes use the centralized `/api/v1` base path.

---

## 3.8 — Gateway Error Handling

**Status:** Implementation completed; additional integration testing remains

### Objective

Provide a consistent JSON error-response structure and avoid exposing internal exception details to API clients.

### Implemented Files

#### 1. `ApiErrorResponse.java`

**Location:**

`api-gateway/src/main/java/com/wearenavodayan/apigateway/exception/ApiErrorResponse.java`

The response record contains:

| Field | Purpose |
|---|---|
| `timestamp` | Time the error response was created |
| `status` | HTTP status code |
| `error` | Error category |
| `message` | Client-facing message |
| `path` | Request path |
| `correlationId` | Request correlation identifier |

#### 2. `ApiErrorResponseWriter.java`

**Location:**

`api-gateway/src/main/java/com/wearenavodayan/apigateway/exception/ApiErrorResponseWriter.java`

The writer serializes error responses as JSON using the Jackson 3 `tools.jackson.databind.ObjectMapper` package used by this Spring Boot 4 application.

It sets the HTTP status, JSON content type, UTF-8 character encoding, and correlation ID in the response body.

#### 3. `GatewayExceptionHandler.java`

**Location:**

`api-gateway/src/main/java/com/wearenavodayan/apigateway/exception/GatewayExceptionHandler.java`

The handler implements Spring MVC's `HandlerExceptionResolver`.

It provides a generic HTTP 500 response with the message:

`An unexpected error occurred.`

Internal exception details are not returned to the client.

### Testing

`ApiErrorResponseWriterTests` cover:

- Writing a JSON error response with HTTP 404.
- Including the request correlation ID.
- Preferring the response correlation ID when it is already present.
- Writing the generic error message for HTTP 500.

### Important Limitation

The tests verify the error-response writer. They do not establish complete end-to-end behavior for every routing failure, downstream 404, connection refusal, timeout, or exception-resolution scenario.

A separate filter that rewrote every `/api/` 404 was removed because it could incorrectly alter legitimate 404 responses returned by downstream services.

The error-handling integration should be tested further before claiming comprehensive production-ready coverage.

### Result

The gateway has a standardized error-response model, a JSON response writer, and a generic exception resolver.

---

## Phase 3 — Testing and Verification

### Targeted Gateway Test Command

The following command was executed after implementing Phase 3.8:

```powershell
mvn -pl api-gateway clean test
```

### Result

The latest recorded test run completed successfully:

| Metric | Result |
|---|---:|
| Total tests | 19 |
| Failures | 0 |
| Errors | 0 |
| Skipped | 0 |
| Build status | BUILD SUCCESS |

The test suite included gateway configuration and filter tests, as well as the error-response writer tests.

Normal Mockito/ByteBuddy dynamic-agent warnings were observed and did not cause the test run to fail.

### Verification Scope

The successful test run confirms the covered configuration and unit-test behavior. It does not replace end-to-end tests for live downstream services, real timeout enforcement, or all exception-resolution scenarios.

---

## Phase 3 — Final Architecture

```text
Web / Mobile Applications
          |
          v
   API Gateway :8080
          |
          +------------------------+
          |            |           |
          v            v           v
     Auth Service   User Service  JNV Service
       :8081          :8082         :8083
          |            |             |
          v            v             v
       auth_db        user_db       jnv_db
```

### Gateway Responsibilities

- Centralized API entry point.
- Request routing.
- Correlation ID generation and propagation.
- CORS policy.
- In-memory request rate limiting.
- Centralized downstream service URL configuration.
- HTTP client timeout configuration.
- API versioning.
- Standardized gateway error responses.
- Actuator health and application information.

The gateway routes requests; authentication and authorization will be implemented in the Auth Service and integrated with protected endpoints in a subsequent phase.

---

## Phase 3 — Final Checklist

| Item | Status |
|---|---|
| API Gateway configuration | Completed |
| Auth, User and JNV routes | Completed |
| Correlation ID request filter | Completed |
| CORS configuration | Completed |
| In-memory rate limiting | Completed |
| Service URLs and timeout properties | Configured; actual timeout behavior needs integration tests |
| Centralized API versioning | Completed |
| Standardized JSON error response | Implemented |
| Gateway exception resolver | Implemented |
| Targeted gateway tests | Passed |
| End-to-end downstream failure and timeout tests | Outstanding |
| Distributed production rate limiting | Future enhancement |

---

## Git History

The following commits are recorded in the backend repository:

| Commit | Description |
|---|---|
| `662945a` | Phase 3.4: Configure CORS for API Gateway |
| `6fac6fc` | Phase 3.5: Configure API Gateway Rate Limiting |
| `3e686e9` | Phase 3.6: Configure Service Communication |
| `063c5a8` | Phase 3.7: Configure API Versioning |
| `ccc6522` | Phase 3.8: Configure Gateway Error Handling |

The repository was confirmed clean and synchronized with `origin/main` after the Phase 3.8 commit.

---

## Outstanding Work After Phase 3

The following items remain relevant to the overall platform:

- Add integration tests for real downstream connection failures and timeout enforcement.
- Verify exception resolution and error responses through live HTTP requests.
- Test gateway behavior when downstream services return 404, 5xx, or malformed responses.
- Consider Redis-backed rate limiting for multi-instance production deployment.
- Configure production-specific service URLs and secure deployment settings.
- Implement authentication and authorization in the Auth Service.

## Phase 3 Conclusion

Phase 3 established the gateway foundation for the We Are Navodayan microservices platform. It includes service routing, request correlation, CORS, in-memory rate limiting, downstream HTTP client configuration, centralized API versioning, and standardized error-response handling.

The targeted API Gateway test suite passed with 19 tests and no failures, errors, or skipped tests. Additional end-to-end testing remains necessary for production confidence.

**Next planned milestone:** Phase 4 — Authentication & Authorization, beginning with authentication-flow design, followed by user registration, password hashing, login, JWT generation and validation, refresh-token rotation, Spring Security integration, role-based authorization, and authentication error handling.

# Phase 4: Authentication & Security

## Objective

Implement a secure, production-oriented authentication and authorization system for the We Are Navodayan platform using Java 21, Spring Boot, Spring Security, JWT, PostgreSQL, Flyway, and BCrypt.

This phase establishes the foundation for secure access across the platform's microservices.

## Technology Stack

- Java 21
- Spring Boot 4.1.1
- Spring Security 7
- Spring OAuth2 Resource Server
- JWT (JSON Web Token)
- PostgreSQL 17
- Spring Data JPA
- Flyway
- BCrypt password hashing
- Maven
- JUnit 5
- Spring Boot Test
- MockMvc

---

## Phase 4.1: Design Authentication Flow

### Goals

- Define registration and login flows.
- Separate authentication credentials from user profile information.
- Define access-token and refresh-token responsibilities.
- Establish public and protected API endpoints.

### Authentication Flow

1. A user registers using their email, password, and full name.
2. The auth service validates the request.
3. The password is hashed using BCrypt.
4. The account is saved in PostgreSQL.
5. The user logs in with their credentials.
6. The service validates the credentials.
7. The service issues a short-lived JWT access token and a refresh token.
8. The client sends the access token in the Authorization header.
9. Spring Security validates the JWT before allowing access to protected endpoints.
10. When the access token expires, the client uses the refresh token to obtain new tokens.

### API Endpoints

| Method | Endpoint | Access |
|---|---|---|
| POST | `/api/v1/auth/register` | Public |
| POST | `/api/v1/auth/login` | Public |
| POST | `/api/v1/auth/refresh` | Public |
| GET | `/api/v1/auth/me` | Authenticated |
| GET | `/api/v1/admin/access` | ADMIN role |
| GET | `/actuator/health` | Public |
| GET | `/actuator/info` | Public |

---

## Phase 4.2: User Registration

### Goals

- Implement registration API.
- Validate incoming registration data.
- Prevent duplicate email registrations.
- Hash passwords before storing them.
- Persist accounts in PostgreSQL.

### Database Table: `user_accounts`

| Column | Description |
|---|---|
| `id` | UUID primary key |
| `email` | Unique email address |
| `password_hash` | BCrypt password hash |
| `full_name` | User's full name |
| `role` | Account role; defaults to `USER` |
| `enabled` | Whether the account is enabled |
| `created_at` | Account creation timestamp |
| `updated_at` | Last update timestamp |

### Implementation Details

- Normalize email addresses by trimming whitespace and converting to lowercase.
- Reject duplicate email addresses.
- Validate required fields and email format.
- Store only the password hash, never the plaintext password.
- Use Flyway to manage schema migrations.
- Use service-layer transaction management.

### Expected Behavior

- Successful registration creates an account.
- Duplicate email returns HTTP `409 Conflict`.
- Invalid request data returns HTTP `400 Bad Request`.
- Passwords are stored as BCrypt hashes.

---

## Phase 4.3: Login and JWT Generation

### Goals

- Authenticate registered users.
- Generate signed JWT access tokens.
- Return access and refresh tokens after successful login.

### JWT Claims

| Claim | Purpose |
|---|---|
| `iss` | Token issuer |
| `sub` | User UUID |
| `aud` | Intended API audience |
| `iat` | Token issue time |
| `exp` | Token expiry time |
| `jti` | Unique token identifier |
| `role` | User role, such as `USER` or `ADMIN` |

### JWT Configuration

- Issuer: `we-are-navodayan-auth`
- Audience: `we-are-navodayan-api`
- Access-token lifetime: 15 minutes
- Refresh-token lifetime: 7 days
- Signing algorithm: HS256

### Security Requirements

- Keep the JWT signing secret outside source control.
- Read the secret from the `JWT_SECRET` environment variable.
- Use a Base64-encoded secret containing at least 32 bytes.
- Never log passwords, access tokens, refresh tokens, or signing secrets.

### Expected Behavior

- Valid credentials return access and refresh tokens.
- Invalid credentials return HTTP `401 Unauthorized`.
- The response does not expose the stored password hash.

---

## Phase 4.4: Password Hashing and Endpoint Protection

### Goals

- Secure password storage.
- Protect private endpoints.
- Validate JWTs on protected requests.

### Password Security

- Use Spring Security's BCrypt password encoder.
- Hash passwords during registration.
- Verify passwords during login using the password encoder.
- Never store or compare plaintext passwords directly.

### Endpoint Protection

- Public endpoints: registration, login, refresh, health, and info.
- Protected endpoints: require a valid JWT.
- Admin endpoints: require the `ADMIN` role.
- Use stateless session management.
- Disable CSRF for the stateless bearer-token API.

### Expected Behavior

- Missing token on a protected endpoint returns HTTP `401`.
- Invalid or expired token returns HTTP `401`.
- Valid token allows access when authorization rules permit it.

---

## Phase 4.5: JWT Generation

### Goals

- Generate signed JWT access tokens using Spring Security's JWT support.
- Populate required claims.
- Set issue and expiration timestamps.
- Include the authenticated user's UUID and role.

### Implementation

- Configure a `JwtEncoder`.
- Use the configured HS256 signing key.
- Generate a unique `jti` for every access token.
- Set the issuer and audience consistently with JWT validation.
- Set the expiration to 15 minutes after issuance.

### Expected Behavior

A successfully authenticated user receives a signed JWT containing the expected claims and a limited lifetime.

---

## Phase 4.6: JWT Validation

### Goals

- Validate incoming access tokens.
- Verify the signature, issuer, audience, and expiration.
- Reject malformed or expired tokens.
- Make the authenticated user's identity available to controllers.

### Implementation

- Configure a `JwtDecoder`.
- Validate the issuer.
- Validate the audience.
- Verify the signature using the configured signing key.
- Enforce token expiration.
- Integrate JWT validation with Spring Security's OAuth2 Resource Server.

### Expected Behavior

- Valid JWT: request proceeds to authorization.
- Invalid JWT: HTTP `401 Unauthorized`.
- Expired JWT: HTTP `401 Unauthorized`.
- Incorrect issuer or audience: HTTP `401 Unauthorized`.

---

## Phase 4.7: Refresh Token Rotation

### Goals

- Allow users to obtain new tokens without logging in again.
- Store refresh-token hashes instead of raw tokens.
- Rotate refresh tokens after successful use.
- Prevent reuse of revoked refresh tokens.

### Database Table: `refresh_tokens`

| Column | Description |
|---|---|
| `id` | UUID primary key |
| `user_id` | Foreign key to `user_accounts.id` |
| `token_hash` | SHA-256 hash of the refresh token |
| `expires_at` | Refresh-token expiration time |
| `revoked` | Whether the token has been revoked |
| `created_at` | Token creation timestamp |

### Refresh Token Flow

1. Generate a cryptographically secure random refresh token.
2. Return the raw token to the client only when issuing it.
3. Store its SHA-256 hash in PostgreSQL.
4. When refreshing, hash the supplied token and locate the stored record.
5. Validate that the token exists, has not expired, and has not been revoked.
6. Revoke the existing refresh token.
7. Issue a new access token and a new refresh token.
8. Store the hash of the new refresh token.

### Security Requirements

- Use cryptographically secure random token generation.
- Never store raw refresh tokens in the database.
- Reject expired, unknown, or revoked tokens.
- Ensure token rotation is transactionally safe.
- Consider concurrent refresh requests and replay detection.
- Use appropriate client-side storage and transport protections.

### Expected Behavior

- Valid refresh token returns a new token pair.
- Invalid refresh token returns HTTP `401`.
- Reusing a revoked token is rejected.
- Old refresh tokens cannot be used after successful rotation.

---

## Phase 4.8: Spring Security Integration

### Goals

- Integrate JWT validation with Spring Security.
- Configure the security filter chain.
- Enforce stateless authentication.
- Test public and protected endpoints.

### Implementation

- Define a `SecurityFilterChain`.
- Disable CSRF for the bearer-token API.
- Configure `SessionCreationPolicy.STATELESS`.
- Permit the required public endpoints.
- Require authentication for all other endpoints by default.
- Integrate the JWT resource server.

### Expected Behavior

- Public endpoints remain accessible without a token.
- Protected endpoints require a valid JWT.
- JWT validation failures are handled by Spring Security.
- No server-side HTTP session is required for authentication.

---

## Phase 4.9: Role-Based Authorization

### Goals

- Enforce authorization based on JWT roles.
- Distinguish ordinary users from administrators.
- Prevent users from accessing administrator-only APIs.

### Roles

- `USER`
- `ADMIN`

### Implementation

- Include the user's role in the JWT's `role` claim.
- Configure `JwtGrantedAuthoritiesConverter` to read the `role` claim.
- Apply the `ROLE_` authority prefix.
- Restrict `/api/v1/admin/**` to users with the `ADMIN` role.
- Require authentication for other protected endpoints.

### Admin Test Endpoint

`GET /api/v1/admin/access`

Successful response:

    {
      "message": "Admin access granted"
    }

### Expected Behavior

| Scenario | Expected status |
|---|---|
| No token | `401 Unauthorized` |
| Invalid token | `401 Unauthorized` |
| Valid USER token | `403 Forbidden` |
| Valid ADMIN token | `200 OK` |

### Authorization Security

- Never trust a role supplied by a request parameter or request body.
- Derive authorities from a validated JWT.
- Restrict administrator-role assignment to trusted server-side workflows.
- Protect administrative APIs with explicit authorization rules.

---

## Phase 4.10: Authentication Error Handling

### Goals

- Standardize security-related error responses.
- Return consistent JSON for authentication and authorization failures.
- Preserve existing registration, login, and refresh-token error handling.

### Standard Error Response

The `ApiErrorResponse` record contains:

| Field | Description |
|---|---|
| `success` | Always `false` for errors |
| `code` | Machine-readable error code |
| `message` | Human-readable message |
| `timestamp` | Error timestamp |
| `path` | Request URI |

### Error Codes

| HTTP status | Error code | Meaning |
|---|---|---|
| `400` | Existing validation error code | Invalid request data |
| `401` | `UNAUTHORIZED` | Missing or invalid access token |
| `401` | `INVALID_CREDENTIALS` | Invalid login credentials |
| `401` | `INVALID_REFRESH_TOKEN` | Invalid refresh token |
| `403` | `FORBIDDEN` | Authenticated user lacks permission |
| `409` | Existing duplicate-email error code | Email already registered |

### Implementation

- Create `SecurityErrorResponseWriter`.
- Serialize error responses as JSON.
- Configure Spring Security's `AuthenticationEntryPoint`.
- Configure Spring Security's `AccessDeniedHandler`.
- Explicitly configure the OAuth2 Resource Server authentication entry point so malformed or invalid bearer tokens receive the standard JSON response.
- Keep existing login and refresh-token exception handlers intact.
- Use the existing `ApiErrorResponse` record.

### Expected Behavior

- Missing access token returns a standard JSON `401`.
- Invalid access token returns a standard JSON `401`.
- Insufficient role returns a standard JSON `403`.
- Invalid login and refresh-token responses preserve their existing error contracts.
- Validation and duplicate-email errors continue using the existing application exception handler.

---

## Testing Strategy

### Integration Tests

The authentication service integration tests cover:

- Successful user registration.
- Duplicate-email rejection.
- Registration validation.
- Successful login.
- Invalid login credentials.
- JWT claims and expiration.
- Access-token validation.
- Missing-token behavior.
- Invalid-token behavior.
- Refresh-token rotation.
- Invalid and reused refresh tokens.
- Protected endpoint access.
- User and administrator authorization.
- Standard security error responses.
- Application context startup.

### Test Execution

Run from the backend repository:

    $env:DB_PASSWORD = "navodayan_local"
    $env:JAVA_TOOL_OPTIONS = "-Duser.timezone=UTC"
    mvn -pl auth-service clean test

---

## Phase 4 Completion Criteria

- All authentication integration tests pass.
- All authorization integration tests pass.
- JWT signature, issuer, audience, and expiration are validated.
- Passwords are stored using BCrypt.
- Refresh tokens are stored as hashes and rotated after use.
- Public and protected endpoints behave correctly.
- User and administrator access restrictions are enforced.
- Authentication and authorization errors follow the expected response format.
- Changes are reviewed, committed, and pushed to `origin/main`.

---

## Git Commit History

| Phase | Commit message |
|---|---|
| 4.1–4.2 | `Phase 4.1-4.2 : Design Authentication Flow & User Registration` |
| 4.3 | `Phase 4.3 : Implement JWT Authentication and Login` |
| 4.4 | `Phase 4.4 : Protect Endpoints and Validate JWT` |
| 4.7 | `Phase 4.7 : Implement Refresh Token Rotation` |
| 4.8 | `Phase 4.8 : Verify Spring Security Integration` |
| 4.9–4.10 | `Phase 4.9-4.10 : Add Authorization and Security Error Handling` |

---

## Final Outcome

Phase 4 establishes the authentication and authorization foundation for We Are Navodayan. The auth service supports account registration, login, JWT-based access, refresh-token rotation, protected APIs, role-based access control, and standardized security error responses.

# Phase 5 — User Profile Service
Project: We Are Navodayan

**Technology Stack:** Java 21, Spring Boot 4.1.1, Spring MVC, Spring Data JPA, Spring Security 7, Spring OAuth2 Resource Server, PostgreSQL 17, Flyway, Maven, JUnit 5, Mockito, MockMvc

**Status:** Phase 5.1–5.10 implementation completed. User Profile Service tests passed with 72 tests, zero failures, zero errors, and zero skipped tests. Changes committed and pushed to `origin/main`.

Latest Commit: `e7bd763` — `Phase 5.10 : Add Profile REST APIs`

---

# Phase 5 Overview

Phase 5 establishes the User Profile Service for the We Are Navodayan platform. It manages alumni profile information separately from authentication credentials and provides the foundation for alumni discovery, networking, mentorship, and community features.

The service uses PostgreSQL for persistence, Flyway for database migrations, Spring Data JPA for database access, and Spring Security for JWT-based endpoint protection.

The User Profile Service runs on port `8082` and integrates with the Auth Service and JNV Service.

## Objectives

- Establish the User Profile Service and its database schema.
- Integrate profile creation with user registration.
- Implement profile completeness calculation.
- Validate profile information and JNV references.
- Add professional and location information.
- Manage profile skills and interests.
- Store profile image metadata.
- Secure profile endpoints using JWT authentication.
- Strengthen profile validation and ownership checks.
- Expose profile retrieval and update APIs.
- Standardize API error responses.
- Verify service behavior through automated tests.

---

# Phase Checklist

| Task | Description | Status |
|---|---|---|
| 5.1 | Establish User Profile Service foundation | Completed |
| 5.2 | Integrate user registration with profile creation | Completed |
| 5.3 | Implement profile completeness calculation | Completed |
| 5.4 | Add JNV lookup and profile validation | Completed |
| 5.5 | Add profession and location to profiles | Completed |
| 5.6 | Implement profile skills and interests | Completed |
| 5.7 | Add profile image metadata | Completed |
| 5.8 | Secure profile routes with JWT | Completed |
| 5.9 | Strengthen profile validation | Completed |
| 5.10 | Add Profile REST APIs | Completed |

---

# 5.1 — Establish User Profile Service Foundation

**Status: Completed**

## Objective

Establish a dedicated microservice for managing user profile information independently of authentication credentials.

## Technology

- Java 21
- Spring Boot 4.1.1
- Spring MVC
- Spring Data JPA
- PostgreSQL 17
- Flyway
- Maven

## Architecture

The User Profile Service manages alumni information, while the Auth Service manages account credentials and authentication.

The authentication account ID is stored as `authUserId` in the user profile.

This separation allows authentication and profile management to evolve independently.

## Database

Database: `user_db`

The database schema is managed through Flyway migrations.

The service uses UUID identifiers for profile records and authentication account references.

## Core Responsibilities

- Create and retrieve user profiles.
- Associate profiles with authentication accounts.
- Persist profile information in PostgreSQL.
- Validate profile data through the service layer.
- Maintain profile creation and update timestamps.
- Manage database schema changes through versioned migrations.

## Result

The User Profile Service foundation provides a dedicated persistence and business-logic layer for alumni profile information.

---

# 5.2 — Integrate User Registration with Profile Creation

**Status: Completed**

## Objective

Automatically create a user profile when a new account is registered through the Auth Service.

## Implementation

Profile creation is initiated through an internal API exposed by the User Profile Service.

**Internal endpoint:**

`POST /internal/api/v1/user-profiles`

The registration workflow supplies the authentication account UUID and the user's full name.

## Registration Flow

1. A user submits a registration request to the Auth Service.
2. The Auth Service validates the registration details.
3. The account is created in the authentication database.
4. The Auth Service initiates profile creation through the internal User Profile Service API.
5. The User Profile Service validates the supplied account ID and full name.
6. A profile is persisted in `user_db`.
7. The profile is associated with the authentication account through `authUserId`.

## Validation and Duplicate Handling

- Authentication account ID is required.
- Full name is required.
- Full name must not exceed 150 characters.
- Duplicate profiles for the same authentication account are prevented.
- An existing profile with matching registration details is handled idempotently.
- An existing profile with conflicting registration details returns a conflict.
- The internal endpoint requires the configured internal service key.

## Result

User registration is integrated with profile creation, establishing the relationship between authentication accounts and user profiles.

---

# 5.3 — Implement Profile Completeness Calculation

**Status: Completed**

## Objective

Calculate a profile completeness percentage to help users identify missing profile information.

## Implementation

File:

`user-service/src/main/java/com/wearenavodayan/userservice/service/ProfileCompletenessCalculator.java`

The calculator evaluates five profile attributes.

| Profile Attribute | Weight |
|---|---:|
| Full name | 20% |
| Bio | 20% |
| Batch year | 20% |
| JNV association | 20% |
| Profile image URL | 20% |
| **Total** | **100%** |

## Calculation Rules

Each completed attribute contributes 20 percentage points.

A profile with all five attributes populated receives 100%.

The calculation is performed using the profile information available to the service.

## Testing

`ProfileCompletenessCalculatorTest` covers five test cases.

The tests verify completeness calculations for different combinations of populated and missing profile attributes.

## Result

Profile completeness is calculated by a dedicated service component and can be included in profile API responses.

---

# 5.4 — Add JNV Lookup and Profile Validation

**Status: Completed**

## Objective

Associate alumni profiles with Jawahar Navodaya Vidyalaya records and validate profile information before persistence.

## Implementation

The User Profile Service integrates with the JNV Service through a dedicated service client.

The JNV association is stored using `jnvId`.

## Validation Rules

- Authentication account ID is required.
- Full name is required.
- Full name must not exceed 150 characters.
- Optional text fields are validated against their configured length limits.
- Batch year must be between 1900 and 2200 when supplied.
- A supplied JNV identifier is validated against the JNV Service.
- Profile image URLs must use HTTP or HTTPS and contain a valid host.

## JNV Association

When a profile includes a JNV identifier, the service validates the association before accepting the profile change.

A profile without a JNV association can retain a null `jnvId`.

## Result

The User Profile Service supports JNV associations and validates profile data before it is persisted.

---

# 5.5 — Add Profession and Location to Profiles

**Status: Completed**

## Objective

Extend user profiles with professional information and current location to support alumni discovery and networking.

## Profile Fields

| Field | Description |
|---|---|
| `profession` | User's profession |
| `organization` | Current organization |
| `jobTitle` | Current job title |
| `currentCity` | Current city |
| `currentState` | Current state |
| `country` | Current country |

## Validation Limits

| Field | Maximum Length |
|---|---:|
| Profession | 100 characters |
| Organization | 150 characters |
| Job title | 150 characters |
| Current city | 100 characters |
| Current state | 100 characters |
| Country | 100 characters |

These fields are optional.

Optional text is normalized before it is stored.

## Benefits

- Supports professional alumni discovery.
- Enables location-based networking.
- Provides information relevant to mentorship.
- Establishes a foundation for future directory filters.

## Result

The profile model supports professional and location information in addition to core identity fields.

---

# 5.6 — Implement Profile Skills and Interests

**Status: Completed**

## Objective

Allow users to maintain skills and interests separately from their core profile attributes.

## Implementation

A dedicated `UserProfileSkillsInterestsService` manages skills and interests.

The service provides operations to:

- Retrieve a user's skills.
- Retrieve a user's interests.
- Replace the complete skills list.
- Replace the complete interests list.

## Validation and Normalization

- Maximum 30 skills per user.
- Maximum 30 interests per user.
- Values are trimmed.
- Duplicate values are removed.
- Values are validated before being persisted.

## Service Methods

- `getSkills(UUID authUserId)`
- `getInterests(UUID authUserId)`
- Replace skills operation.
- Replace interests operation.

## Testing

`UserProfileSkillsInterestsServiceTest` covers 11 test cases.

## Benefits

Skills and interests establish a foundation for:

- Alumni discovery.
- Mentorship matching.
- Professional networking.
- Community recommendations.
- Interest-based connections.

## Result

Skills and interests are managed through a dedicated service component and can be included in profile responses.

---

# 5.7 — Add Profile Image Metadata

**Status: Completed**

## Objective

Establish support for profile image metadata as a foundation for future image uploads and object storage integration.

## Implementation

Profile image metadata is managed through the profile image metadata functionality.

The database schema includes profile image metadata introduced through Flyway migration V5.

## Image Validation

- Profile image URL is optional.
- Blank optional values are normalized.
- Nonblank URLs must use HTTP or HTTPS.
- URLs must contain a valid host.
- Invalid or unsupported URL schemes are rejected.

## Storage Considerations

The current implementation supports profile image metadata.

**Actual image upload to Amazon S3 is not implemented as part of this phase.**

S3 upload integration, secure upload authorization, image validation, and image lifecycle management remain future work.

## Testing

`ProfileImageMetadataServiceTest` covers seven test cases.

## Result

The User Profile Service has the metadata foundation required for future profile image storage integration.

---

# 5.8 — Secure Profile Routes with JWT

**Status: Completed**

## Objective

Protect profile APIs using JWT authentication and prevent unauthenticated access to protected profile operations.

## Technology

- Spring Security 7
- Spring OAuth2 Resource Server
- JWT
- Stateless security configuration

## JWT Configuration

The User Profile Service validates access tokens using the configured JWT secret.

| Setting | Value |
|---|---|
| Issuer | `we-are-navodayan-auth` |
| Audience | `we-are-navodayan-api` |
| Signing algorithm | HS256 |
| Identity claim | `sub` |
| Secret source | `JWT_SECRET` environment variable |

The JWT subject contains the authentication account UUID.

The service resolves the authenticated account ID from the validated JWT subject.

## Security Rules

- Profile APIs require authentication.
- Invalid or expired JWTs are rejected.
- The service uses stateless authentication.
- Health and information endpoints are public according to the security configuration.
- Internal profile creation is restricted through the internal service-key check.
- Other internal endpoints remain protected.

## Secret Management

The JWT secret is supplied through environment configuration rather than committed to source control.

The Base64-decoded signing secret must contain at least 32 bytes.

Production secrets must be generated and managed securely.

## Testing

`UserServiceJwtSecurityIntegrationTests` covers nine test cases.

## Result

The User Profile Service validates JWTs and establishes the authenticated identity used by profile operations.

---

# 5.9 — Strengthen Profile Validation

**Status: Completed**

## Objective

Strengthen service-layer validation and ensure that profile updates preserve the relationship between a profile and its authentication account.

## Validation

The service validates:

- Required authentication account ID.
- Required full name.
- Text-field maximum lengths.
- Batch year boundaries.
- Profile image URL format.
- JNV association when supplied.
- Profile existence.
- Profile ownership during updates.

## Profile Ownership

The authentication account ID associated with an existing profile cannot be changed through the update operation.

The update operation checks that the existing profile and the submitted candidate profile belong to the same authentication account.

## Normalization

Text values are normalized before persistence.

Optional text fields can be cleared by submitting null or blank values, subject to the existing service validation and normalization rules.

## Profile Update Safety

The REST controller constructs a separate candidate profile for validation and update instead of modifying the managed entity before validation.

This prevents invalid input from mutating the existing managed entity before the service validates the requested changes.

## Database and Transaction Testing

The implementation includes transaction-related tests for profile persistence and update behavior.

`UserProfileServiceTest` covers 17 test cases.

`UserProfileTransactionTests` covers five test cases.

## Result

Profile updates enforce ownership consistency and use the existing business validation rules before persistence.

---

# 5.10 — Add Profile REST APIs

**Status: Completed**

## Objective

Expose profile retrieval and update operations through authenticated REST endpoints for integration with the web and mobile applications.

## Implementation

Controller:

`user-service/src/main/java/com/wearenavodayan/userservice/controller/UserProfileController.java`

Request DTO:

`user-service/src/main/java/com/wearenavodayan/userservice/dto/request/UserProfileUpdateRequest.java`

Response DTO:

`user-service/src/main/java/com/wearenavodayan/userservice/dto/response/UserProfileResponse.java`

Exception handler:

`user-service/src/main/java/com/wearenavodayan/userservice/exception/GlobalExceptionHandler.java`

## API Endpoints

Base path:

`/api/v1/user-profiles`

All three profile endpoints require a valid JWT.

### 1. Get the Authenticated User's Profile

**Method:** GET

**Endpoint:**

`GET /api/v1/user-profiles/me`

Purpose:

Retrieve the profile associated with the authentication account in the JWT subject.

Successful response:

HTTP 200 OK

The response includes the user's profile information, skills, interests, profile completeness, and timestamps.

### 2. Update the Authenticated User's Profile

**Method:** PUT

**Endpoint:**

`PUT /api/v1/user-profiles/me`

Purpose:

Update the editable profile fields for the authenticated user.

The authentication account ID is taken from the existing profile and is not accepted as a mutable field in the request DTO.

The service validates the candidate profile before applying the update.

**Update semantics:** This endpoint uses full-replacement semantics. Clients should send the complete set of editable profile fields. Omitted properties deserialize as null and may clear existing optional values.

Successful response:

HTTP 200 OK

### 3. Get a Profile by ID

**Method:** GET

**Endpoint:**

`GET /api/v1/user-profiles/{id}`

Purpose:

Retrieve a profile using its profile UUID.

This supports authenticated profile lookup for alumni directory and networking use cases.

The endpoint requires authentication, but it does not implement profile-visibility preferences or a separate public-versus-private profile policy.

Before production deployment, profile visibility and privacy rules should be defined and enforced.

## Request DTO

`UserProfileUpdateRequest` includes:

- `fullName`
- `bio`
- `batchYear`
- `jnvId`
- `profileImageUrl`
- `profession`
- `organization`
- `jobTitle`
- `currentCity`
- `currentState`
- `country`

The request does not expose authentication account ownership as an editable field.

## Response DTO

`UserProfileResponse` includes:

- Profile UUID.
- Full name.
- Bio.
- Batch year.
- JNV UUID.
- Profile image URL.
- Profession.
- Organization.
- Job title.
- Current city.
- Current state.
- Country.
- Skills.
- Interests.
- Profile completeness percentage.
- Creation timestamp.
- Last update timestamp.

Internal image storage metadata is not included in this response DTO.

## Standardized Error Handling

The global exception handler returns the existing `ApiResponse` envelope.

Response structure:

    {
      "success": false,
      "data": null,
      "message": "Error description"
    }

Implemented mappings:

| Exception Category | HTTP Status |
|---|---|
| Entity not found | 404 Not Found |
| Illegal argument or validation error | 400 Bad Request |
| Illegal state or conflict | 409 Conflict |
| Response status exception | Corresponding HTTP status |
| Missing or invalid JSON | 400 Bad Request |
| Missing resource or endpoint | 404 Not Found |
| Unexpected exception | 500 Internal Server Error |

Unexpected exceptions return a generic client-facing message rather than exposing internal exception details.

## Testing

`UserProfileControllerTest` covers seven test cases.

`GlobalExceptionHandlerTest` covers five test cases.

The tests verify controller behavior and consistent error-response handling.

## Result

The User Profile Service exposes authenticated profile retrieval and update APIs with response DTOs and standardized application error responses.

---

# Phase 5 — Testing and Verification

## Test Execution

Run the following commands from the backend repository:

    $env:DB_PASSWORD = "navodayan_local"
    $env:JAVA_TOOL_OPTIONS = "-Duser.timezone=UTC"
    $env:JWT_SECRET = [Convert]::ToBase64String(
        [System.Text.Encoding]::UTF8.GetBytes("0123456789abcdef0123456789abcdef")
    )

    mvn -pl user-service clean test

The JWT secret shown above is a local test-only value. Do not use it as a production secret.

## Latest Recorded Test Results

| Test Class | Tests | Failures | Errors |
|---|---:|---:|---:|
| UserProfileControllerTest | 7 | 0 | 0 |
| GlobalExceptionHandlerTest | 5 | 0 | 0 |
| ProfileCompletenessCalculatorTest | 5 | 0 | 0 |
| ProfileImageMetadataServiceTest | 7 | 0 | 0 |
| UserProfileServiceTest | 17 | 0 | 0 |
| UserProfileSkillsInterestsServiceTest | 11 | 0 | 0 |
| UserProfileTransactionTests | 5 | 0 | 0 |
| UserServiceApplicationTests | 6 | 0 | 0 |
| UserServiceJwtSecurityIntegrationTests | 9 | 0 | 0 |
| **Total** | **72** | **0** | **0** |

**Build Status:** BUILD SUCCESS

**Skipped Tests:** 0

The recorded run completed successfully against PostgreSQL 17.11 with Flyway schema version 5.

Mockito/ByteBuddy dynamic-agent warnings and a duplicate-key warning during a database test were observed. They did not cause the test suite to fail.

## Verification Scope

The successful test run verifies the compilation and behavior covered by the 72 tests.

It does not establish complete production readiness for every integration scenario, including:

- End-to-end authentication registration-to-profile creation under service failures.
- Public profile visibility and privacy enforcement.
- Profile image uploads to S3.
- Production deployment configuration.
- Load and performance behavior.
- Distributed rate limiting and other gateway concerns.

These should be addressed as the corresponding platform capabilities are implemented.

---

# Phase 5 — Final Architecture

    Web Application / Mobile Application
                  |
                  v
          API Gateway :8080
                  |
                  v
            Auth Service :8081
                  |
                  | Internal profile creation
                  v
           User Service :8082
                  |
                  v
             user_db
                  |
                  | JNV validation through service client
                  v
             JNV Service :8083
                  |
                  v
              jnv_db

The Auth Service manages credentials and authentication. The User Profile Service manages profile data and associated skills and interests. The JNV Service provides JNV records used to validate profile associations.

## User Profile Service Responsibilities

- Profile persistence and retrieval.
- Association with authentication accounts.
- Profile completeness calculation.
- Profile validation and normalization.
- JNV association validation.
- Professional and location information.
- Skills and interests management.
- Profile image metadata.
- JWT authentication.
- Profile ownership validation.
- Authenticated profile retrieval and update APIs.
- Standardized error responses.
- Database migration management.

---

# Phase 5 — Final Checklist

| Item | Status |
|---|---|
| User Profile Service foundation | Completed |
| Profile creation integration | Completed |
| Profile completeness calculation | Completed |
| JNV lookup and validation | Completed |
| Profession and location fields | Completed |
| Skills and interests | Completed |
| Profile image metadata | Completed |
| JWT-protected profile routes | Completed |
| Profile validation and ownership checks | Completed |
| Profile REST APIs | Completed |
| Standardized API error responses | Completed |
| Unit and integration tests | Passed |
| 72 tests with zero failures or errors | Passed |
| Changes committed | Completed |
| Changes pushed to `origin/main` | Completed |

---

# Git History

The following Phase 5 commits are recorded in the backend repository:

| Commit | Description |
|---|---|
| `a2cb585` | Phase 5.2 : Integrate User Registration with Profile Creation |
| `26fce4b` | Phase 5.3 : Add Profile Completeness Calculation |
| `933ff2c` | Phase 5.4 : Add JNV Lookup and Profile Validation |
| `6d0dbb6` | Phase 5.5 : Add Profession and Location to Profiles |
| `85c6936` | Phase 5.6 : Add Profile Skills and Interests |
| `ea1ff5b` | Phase 5.7 : Add Profile Image Metadata |
| `e057241` | Phase 5.8 : Secure Profile Routes with JWT |
| `2340b4e` | Phase 5.9 : Strengthen Profile Validation |
| `e7bd763` | Phase 5.10 : Add Profile REST APIs |

The latest recorded commit was pushed to `origin/main`.

Note: The Phase 5.1 commit is not included in the history above because its commit identifier and message were not confirmed in the available project record.

---

# Outstanding Work After Phase 5

The following improvements remain relevant to the overall platform:

1. Implement the web application's authentication flow.
2. Integrate the web profile page with the profile REST APIs.
3. Define and enforce profile visibility and privacy rules.
4. Implement profile image upload and storage through Amazon S3.
5. Complete the JNV directory service and web directory integration.
6. Add broader end-to-end tests for cross-service registration and profile creation.
7. Add production-specific configuration, monitoring, and deployment verification.
8. Add profile pagination and filtering as the alumni directory grows.
9. Define appropriate API-level rate limits and abuse protections.
10. Review database constraint violations and error mappings for consistent client-facing behavior.

---

# Phase 5 Conclusion

Phase 5 establishes the User Profile Service as the foundation for alumni identity and professional networking in We Are Navodayan.

The service now supports profile creation integration, profile completeness, JNV association validation, professional and location fields, skills and interests, image metadata, JWT-protected routes, profile validation, authenticated profile retrieval, and profile updates.

The latest recorded test run passed all 72 tests with no failures, errors, or skipped tests. The Phase 5.10 implementation was committed and pushed to `origin/main` as `e7bd763`.

The implementation is a solid foundation for the next stage of the platform, while privacy policy enforcement, S3 image uploads, broader end-to-end testing, and production hardening remain future work.
