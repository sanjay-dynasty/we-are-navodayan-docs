# We Are Navodayan — Simplified Infrastructure Development Roadmap

## Phase 1 — Foundation & Infrastructure as Code

### 1.1 Infrastructure Requirements
- Define application infrastructure requirements.
- Finalize the cost-conscious AWS architecture.
- Define expected traffic and scalability requirements.

### 1.2 AWS Foundation
- Configure AWS CLI and IAM.
- Configure AWS profiles.
- Select AWS region (`ap-south-1`).
- Define environment strategy.
- Establish naming conventions and resource tags.

### 1.3 CDK Project Setup
- Initialize AWS CDK with TypeScript.
- Configure CDK context and environment settings.
- Define stack structure and reusable constructs.
- Configure infrastructure outputs.
- Configure CDK synthesis and diff workflows.

### 1.4 Infrastructure Validation
- Write CDK unit tests.
- Validate generated CloudFormation templates.
- Review infrastructure changes before deployment.
- Bootstrap the AWS environment.

---

## Phase 2 — Minimal VPC Networking

### 2.1 Network Architecture
- Define VPC architecture and CIDR ranges.
- Configure two Availability Zones.
- Define public, application, and database subnet tiers.
- Review network design against the cost budget.

### 2.2 VPC and Subnets
- Create the VPC.
- Configure public subnets.
- Configure private application subnets.
- Configure isolated database subnets.
- Configure the Internet Gateway.

### 2.3 Routing
- Configure public subnet route tables.
- Configure private application subnet routing.
- Configure database subnet routing.
- Verify internet access and isolation requirements.

### 2.4 Network Security
- Configure security groups.
- Restrict database access to the backend.
- Review default network ACLs.
- Add VPC endpoints only when justified by cost and requirements.

### 2.5 Network Validation
- Test subnet configuration and routing.
- Validate security group rules.
- Verify database isolation.
- Review the need for NAT Gateway and VPC Flow Logs before enabling them.

---

## Phase 3 — Security & Secrets

### 3.1 IAM Foundation
- Define IAM roles for infrastructure and application services.
- Configure least-privilege IAM policies.
- Configure ECS task execution and application task roles.
- Restrict access to AWS resources.

### 3.2 Secrets Management
- Select AWS Secrets Manager or SSM Parameter Store as appropriate.
- Store database credentials securely.
- Store JWT signing keys and application secrets.
- Configure access to secrets from the backend.
- Keep credentials out of source control.

### 3.3 Encryption and HTTPS
- Configure encryption for supported AWS resources.
- Define database encryption settings.
- Prepare TLS certificates for HTTPS.
- Enforce HTTPS for public application endpoints.

### 3.4 Security Validation
- Review IAM permissions.
- Validate security group rules.
- Verify secret access restrictions.
- Check public access settings for storage resources.
- Review essential AWS audit and security settings.

---

## Phase 4 — PostgreSQL Database Infrastructure

### 4.1 Database Design
- Define database requirements.
- Select an appropriate RDS PostgreSQL instance size.
- Estimate storage and monthly database costs.
- Decide on single-AZ or Multi-AZ deployment.

### 4.2 RDS Setup
- Create an RDS PostgreSQL instance.
- Configure database subnet groups.
- Place the database in private or isolated subnets.
- Configure the database security group.
- Enable encryption.

### 4.3 Database Configuration
- Configure database credentials.
- Integrate secrets management.
- Configure storage and backup retention.
- Configure essential maintenance settings.
- Review database connectivity requirements.

### 4.4 Backend Connectivity
- Configure Spring Boot database properties.
- Configure connection pooling.
- Validate database connectivity from the backend.
- Test migrations and schema initialization.

### 4.5 Database Validation
- Verify that public database access is disabled.
- Test authorized database connectivity.
- Verify automated backups.
- Document the database recovery procedure.

---

## Phase 5 — Backend Deployment

### 5.1 Containerization
- Define the backend container architecture.
- Create Dockerfiles for required Spring Boot services.
- Configure multi-stage Docker builds.
- Configure application health checks.
- Test containers locally.

### 5.2 Container Registry
- Create Amazon ECR repositories.
- Configure image tagging.
- Push application images to ECR.
- Enable image scanning where appropriate.

### 5.3 Compute Platform
- Create an ECS cluster.
- Configure ECS Fargate task definitions.
- Configure CPU and memory settings.
- Configure environment variables and secret injection.
- Deploy the required backend services.
- Configure logging and health checks.

### 5.4 API Entry Point
- Select a suitable API entry architecture.
- Configure an Application Load Balancer or another suitable API entry service.
- Configure target groups and health checks where applicable.
- Configure HTTPS and API routing.
- Configure CORS and application-level rate limiting.

### 5.5 Backend Validation
- Verify application health.
- Test authentication and authorization.
- Validate database connectivity.
- Test API endpoints.
- Verify application logs and error handling.
- Review deployment and compute costs.

---

## Phase 6 — React Website Deployment

### 6.1 Frontend Build
- Configure production environment variables.
- Configure the backend API base URL.
- Build the React application.
- Verify production assets and routing.

### 6.2 Static Hosting
- Create an S3 bucket for frontend assets.
- Configure private bucket access.
- Configure CloudFront distribution.
- Configure Origin Access Control.
- Prevent direct public access to the origin bucket.

### 6.3 HTTPS and Caching
- Configure HTTPS through CloudFront.
- Configure cache policies.
- Configure compression.
- Configure SPA routing and error handling.
- Define cache invalidation procedures.

### 6.4 Website Deployment
- Upload production assets to S3.
- Configure CloudFront invalidation.
- Verify website access.
- Test authentication and API integration.
- Validate website behavior on desktop and mobile browsers.

---

## Phase 7 — Domain & Media

### 7.1 Domain Configuration
- Define the domain and subdomain strategy.
- Configure DNS records.
- Configure the frontend domain.
- Configure the API domain.
- Validate TLS certificates.
- Verify HTTPS redirects and DNS resolution.

### 7.2 Media Storage
- Create a separate S3 bucket for application uploads if required.
- Configure Block Public Access.
- Configure encryption.
- Define the media storage structure.
- Configure lifecycle policies where useful.

### 7.3 Media Access
- Implement authorized media upload and download flows.
- Configure pre-signed URLs where appropriate.
- Configure S3 CORS for browser uploads.
- Validate access permissions.
- Prevent unauthorized access to private media.

### 7.4 Media Delivery
- Decide whether CloudFront is required for uploaded media.
- Configure caching if beneficial.
- Test profile image and community media workflows.
- Review storage and data transfer costs.

---

## Phase 8 — CI/CD Pipeline

### 8.1 Pipeline Design
- Define the GitHub Actions workflow.
- Separate build, test, and deployment stages.
- Define deployment permissions.
- Establish a controlled deployment process.

### 8.2 AWS Authentication
- Configure GitHub Actions OIDC with AWS.
- Create a restricted deployment role.
- Configure role trust conditions.
- Avoid long-lived AWS access keys in GitHub secrets.

### 8.3 Backend Pipeline
- Build Spring Boot services.
- Run automated tests.
- Build Docker images.
- Publish images to ECR.
- Deploy approved changes to ECS.
- Verify deployment health.

### 8.4 Frontend Pipeline
- Install dependencies.
- Run frontend tests and build.
- Upload assets to S3.
- Invalidate CloudFront when required.
- Verify website deployment.

### 8.5 Infrastructure Pipeline
- Run CDK build and tests.
- Run CDK synthesis.
- Review infrastructure diffs.
- Require approval before production infrastructure changes.
- Deploy approved changes.
- Document rollback procedures.

---

## Phase 9 — Monitoring & Cost Controls

### 9.1 Application Monitoring
- Configure CloudWatch Logs.
- Configure backend application logs.
- Monitor application errors.
- Monitor service health and availability.
- Configure essential CloudWatch alarms.

### 9.2 Infrastructure Monitoring
- Monitor ECS service health and resource utilization.
- Monitor RDS storage, connections, and CPU.
- Monitor load balancer and API errors where applicable.
- Review S3 and CloudFront usage.
- Configure alerts for important failures.

### 9.3 Cost Management
- Configure AWS Budgets.
- Configure billing alerts.
- Apply consistent resource tags.
- Review monthly service costs.
- Identify idle and unnecessary resources.
- Review data transfer, logging and storage charges.

### 9.4 Operational Readiness
- Document common operational tasks.
- Define basic incident response steps.
- Document backup verification.
- Document secret and dependency update procedures.
- Review infrastructure health periodically.

---

## Phase 10 — Production Verification

### 10.1 Security Verification
- Verify HTTPS.
- Test authentication and authorization.
- Verify database and storage access restrictions.
- Check secret handling.
- Review IAM permissions.
- Scan application dependencies and container images.

### 10.2 Functional Verification
- Test user registration and login.
- Test profile management.
- Test directory and community features.
- Test media upload and retrieval.
- Verify frontend-to-backend integration.
- Validate error handling.

### 10.3 Performance Verification
- Test important API endpoints.
- Measure response times.
- Test database queries and connection pooling.
- Run a realistic load test.
- Verify resource utilization under load.
- Adjust compute and database sizing based on results.

### 10.4 Backup and Recovery
- Verify database backup configuration.
- Test database restoration.
- Document recovery steps.
- Define acceptable downtime and data-loss targets.
- Review the need for additional disaster recovery resources.

### 10.5 Deployment Verification
- Verify frontend and backend deployments.
- Test health checks.
- Test rollback procedures.
- Confirm monitoring and budget alerts.
- Review final infrastructure costs.
- Complete the production readiness checklist.

---

## Deferred Infrastructure — Add Only When Required

The following components are not part of the minimum initial deployment:

- Amazon ElastiCache for Redis.
- Amazon MSK for Kafka.
- Amazon SQS and SNS.
- AWS Lambda for optional background tasks.
- AWS WAF and advanced traffic protection.
- NAT Gateway and additional VPC endpoints.
- Multi-AZ RDS and advanced disaster recovery.
- Complex auto-scaling policies.
- Distributed tracing and advanced observability.
- Separate staging AWS environment.

Introduce these components when actual traffic, reliability requirements, or application functionality justify their operational complexity and cost.

## Cost and Deployment Policy

- Do not deploy infrastructure before reviewing estimated monthly costs.
- Prefer small, appropriately sized resources during initial development.
- Use local development and CDK synthesis before provisioning AWS resources.
- Keep database and application secrets out of Git.
- Review actual AWS charges after deployment.
- Scale resources based on measurements rather than the maximum registered-user estimate alone.

**Target outcome:** A maintainable React and Spring Boot platform for a community of fewer than 100,000 users, using only the AWS infrastructure needed to run the application reliably.