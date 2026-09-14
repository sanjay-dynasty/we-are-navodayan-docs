
### `docs/architecture/decisions.md`

```md
# We Are Navodayan — Architecture Decisions

## ADR-001 — Microservices

**Decision:** Use microservices for the backend.

**Reason:**
- Independent deployment
- Independent scaling
- Clear ownership
- Enterprise architecture experience

---

## ADR-002 — Spring Boot

**Decision:** Use Java + Spring Boot.

**Reason:**
- Enterprise adoption
- Strong ecosystem
- Spring Security
- AWS compatibility

---

## ADR-003 — Kafka

**Decision:** Use Kafka for event-driven communication.

**Production:** Amazon MSK

**Reason:**
- Event streaming
- Loose coupling
- Multiple consumers
- Asynchronous processing

---

## ADR-004 — REST + Kafka

**Decision:** Use REST for synchronous communication and Kafka for
asynchronous/event-driven workflows.

---

## ADR-005 — PostgreSQL

**Decision:** Use PostgreSQL for transactional data.

**Reason:**
- Relational domain
- Strong consistency
- Mature ecosystem

---

## ADR-006 — Redis

**Decision:** Use Redis for caching and high-speed temporary data.

---

## ADR-007 — AWS

**Decision:** Deploy the platform on AWS.

**Reason:**
- Production cloud experience
- Scalable infrastructure
- Enterprise-grade services

---

## ADR-008 — AWS CDK

**Decision:** Use AWS CDK for Infrastructure as Code.

**Reason:**
- Version-controlled infrastructure
- Reproducible environments
- Type-safe AWS infrastructure

---

## ADR-009 — Docker

**Decision:** Containerize backend services using Docker.

**Reason:**
- Consistent environments
- Independent deployments
- ECS compatibility

---

## ADR-010 — Technology Selection

Every technology must have a clear business or engineering purpose.

The project should demonstrate enterprise concepts without unnecessary
complexity or infrastructure.