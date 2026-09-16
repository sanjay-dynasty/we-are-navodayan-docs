# Backend Development Details

## Phase 0 — Project & Development Setup

### B0.1 — Understand Backend Requirements

Defined the backend architecture and initial microservice boundaries.

Architecture:

    Web / Mobile
          ↓
      API Gateway
          ↓
    Spring Boot Services
          ↓
    PostgreSQL / Redis / Kafka / AWS

Communication:

- REST — synchronous communication
- Kafka — asynchronous event-driven communication

Initial services:

- API Gateway
- Auth Service
- User Service
- JNV Service
- Alumni Service
- Community Service
- Opportunity Service
- Mentorship Service
- Event Service
- Notification Service

---

### B0.2 — Install Java & Required Tools

Installed and configured the backend development environment.

Tools:

- Java 21 LTS
- Maven 3.9.16
- Git
- VS Code
- Docker Desktop
- Docker Compose
- WSL 2
- Ubuntu

Configured:

    JAVA_HOME
    MAVEN_HOME

Verification:

    java -version
    mvn -version
    git --version
    docker --version
    docker compose version
    docker run --rm hello-world

Java 21 was configured as the active Java version.

Docker Engine and WSL 2 integration were verified successfully.

---

### B0.3 — Configure IDE & Development Environment

Configured VS Code for Java and Spring Boot development.

Installed extensions:

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

Verified from VS Code terminal:

    java -version
    mvn -version
    $env:JAVA_HOME
    git --version
    docker --version
    docker compose version

Skipped `.vscode/settings.json` and `.vscode/extensions.json`.

---

### B0.4 — Create Spring Boot Project Structure

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

The individual Spring Boot services will be created in B0.8.

---

### B0.5 — Configure Maven

Configured the root Maven `pom.xml`.

Configured:

- Group ID: `com.we-are-navodayan`
- Artifact ID: `we-are-navodayan-backend`
- Version: `0.0.1-SNAPSHOT`
- Packaging: `pom`
- Java: `21`
- Maven Compiler Release: `21`
- Maven Compiler Plugin: `3.14.1`

Maven compiler configuration:

    <maven.compiler.release>21</maven.compiler.release>

    maven-compiler-plugin
    version: 3.14.1

Verification:

    mvn help:effective-pom -N

Result:

    BUILD SUCCESS

Effective POM confirmed Java 21 and compiler release 21.

---

### B0.6 — Configure Git Workflow

Initialized Git repository and configured `main` as the primary branch.

Commands:

    git init
    git branch -M main

Configured Git identity:

    git config user.name "Sanjay Kumar"
    git config user.email "ersanjay426@gmail.com"

Added initial files:

    git add .

Created Phase 0 commit:

    git commit -m "Phase 0 : Project & Development Setup"

Commit:

    013312d

Configured GitHub remote:

    git remote add origin https://github.com/sanjay-dynasty/we-are-navodayan-backend.git

Pushed the repository:

    git push -u origin main

Result:

    main → origin/main

## Phase 0 Overall

Completed the backend development foundation:

- Defined microservice architecture
- Installed Java 21 and required tools
- Configured VS Code
- Created backend repository structure
- Configured root Maven project
- Initialized Git
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
| Backend structure | ✅ |
| Root Maven POM | ✅ |
| Maven effective POM | ✅ |
| Git repository | ✅ |
| Main branch | ✅ |
| Initial commit | ✅ |
| GitHub remote | ✅ |
| GitHub push | ✅ |

## Phase 0 Status

**Completed**

## Phase 0 Commit

    git commit -m "Phase 0 : Project & Development Setup"