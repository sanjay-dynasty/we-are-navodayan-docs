# We Are Navodayan — Infrastructure Foundation

# Phase 0: Infrastructure & Cloud Foundation

This phase establishes the foundation for managing AWS infrastructure for the We Are Navodayan platform. It covers infrastructure requirements, AWS account setup, CLI configuration, IAM, AWS profiles, region selection, environment strategy, naming conventions, resource tagging, and repository structure.

The infrastructure will be managed using AWS CDK with TypeScript. Application infrastructure will be provisioned incrementally after reviewing security, configuration, and expected costs.

## 0.1 Understand Infrastructure Requirements

The infrastructure will support the We Are Navodayan web application, backend microservices, database, caching, media storage, and supporting services.

### Technology Stack

- **Backend:** Java 21, Spring Boot, microservices.
- **Frontend:** React and TypeScript.
- **Database:** PostgreSQL.
- **Caching:** Redis.
- **Infrastructure as Code:** AWS CDK with TypeScript.
- **Container Hosting:** Amazon ECS.
- **Networking:** Amazon VPC and Application Load Balancer.
- **Storage and Content Delivery:** Amazon S3 and CloudFront.
- **Monitoring:** Amazon CloudWatch.
- **Secrets Management:** AWS Secrets Manager.
- **Messaging:** Amazon SQS/SNS and Kafka infrastructure if required.

### Planned AWS Services

| AWS Service | Purpose |
|---|---|
| AWS IAM | Identity and access management |
| AWS CDK | Infrastructure as Code |
| Amazon VPC | Network isolation |
| Amazon ECS | Containerized backend hosting |
| Application Load Balancer | Application traffic routing |
| Amazon RDS PostgreSQL | Relational database |
| Amazon ElastiCache | Redis caching |
| Amazon MSK | Kafka infrastructure, if required |
| Amazon S3 | Media and file storage |
| Amazon CloudFront | Content delivery |
| Amazon CloudWatch | Logging, metrics, and monitoring |
| AWS Secrets Manager | Secure application secrets |
| Amazon SQS/SNS | Messaging and notifications |
| AWS Lambda | Serverless workloads, if required |

### Development and Cost Principles

- Prefer local development wherever practical.
- Review AWS pricing before provisioning resources.
- Avoid deploying paid resources before reviewing expected costs.
- Use secure credentials and least-privilege permissions.
- Review infrastructure changes before deployment.
- Keep environment-specific configuration separate.

No application infrastructure resources were provisioned during the initial repository setup.

## 0.2 Define AWS Account Structure

An existing personal AWS account is being used for initial development.

A dedicated IAM user named `navodayan-dev` was created for AWS CLI operations. Routine development should not use root credentials.

The initial setup uses one AWS account. Development, staging, and production will be logically separated through configuration and resource naming. Separate AWS accounts may be introduced later if stronger isolation is required.

### Verify AWS Identity

Run the following command after configuring valid AWS credentials:

```powershell
aws sts get-caller-identity --profile navodayan-dev
```

A successful response contains the authenticated user ID, account ID, and ARN.

Example response structure:

```json
{
  "UserId": "REDACTED",
  "Account": "REDACTED",
  "Arn": "arn:aws:iam::REDACTED:user/navodayan-dev"
}
```

This command verifies which AWS identity is being used by the selected CLI profile.

### Security Requirements

- Do not use root credentials for routine development.
- Never commit access keys, secret access keys, session tokens, or other credentials.
- Enable MFA where possible.
- Prefer temporary credentials when practical.
- Deactivate and replace exposed credentials immediately.
- Review IAM permissions before deploying infrastructure.

**Credential incident:** The AWS access key ID and secret access key were pasted into a chat during initial setup. Those credentials must be treated as compromised, deactivated, and replaced before further use. Do not include their actual values in documentation or Git.

## 0.3 Configure AWS CLI

AWS CLI v2 was installed on the Windows development machine.

### Verify Installation

```powershell
aws --version
```

The installation was verified as AWS CLI v2.

### Configure AWS CLI Credentials

The following command was used during initial configuration:

```powershell
aws configure --profile navodayan-dev
```

The CLI prompts for:

- AWS Access Key ID
- AWS Secret Access Key
- Default region name
- Default output format

Use valid credentials entered directly into the local CLI prompt. Never store credentials in source code or documentation.

The default region is `ap-south-1`, and the output format is `json`.

### Verify Authentication

```powershell
aws sts get-caller-identity --profile navodayan-dev
```

If the command returns `NoCredentials`, the CLI cannot locate usable credentials for the selected profile. Configure a supported authentication method before proceeding.

After replacing the exposed access key, rerun the identity verification command.

## 0.4 Configure AWS IAM

The IAM user created for this project is:

```text
navodayan-dev
```

IAM determines which AWS operations this user can perform.

### Inspect IAM Configuration

In the AWS Console:

1. Open IAM.
2. Navigate to Users.
3. Select `navodayan-dev`.
4. Review the attached permissions.
5. Open Security credentials.
6. Review access keys and MFA configuration.

The initial inspection showed that the IAM user had no attached policies and no MFA device assigned. Root MFA was enabled, and no root access keys were present at the time of inspection.

IAM Identity Center SSO was investigated but was not enabled in the account during initial setup.

### IAM Security Principles

- Apply least-privilege permissions.
- Grant only the permissions needed for the required tasks.
- Avoid broad administrator permissions without reviewing the risks.
- Enable MFA where possible.
- Protect credentials and replace compromised keys.
- Review permissions before CDK bootstrap and deployment.

The IAM user must have appropriate permissions before it can create or modify AWS resources. Authentication alone does not grant permission to deploy infrastructure.

## 0.5 Configure AWS Profiles

AWS CLI profiles allow multiple AWS configurations to coexist on the development machine.

The project profile is:

```text
navodayan-dev
```

The configured region is `ap-south-1`, and the default output format is `json`.

### List Profiles

```powershell
aws configure list-profiles
```

The output should include:

```text
navodayan-dev
```

### Inspect Profile Configuration

```powershell
aws configure list --profile navodayan-dev
```

This command displays the configuration source for the selected profile. Do not share output containing sensitive credential information.

### Verify Region

```powershell
aws configure get region --profile navodayan-dev
```

Expected output:

```text
ap-south-1
```

### Verify Identity

```powershell
aws sts get-caller-identity --profile navodayan-dev
```

Use `--profile navodayan-dev` explicitly in project-related AWS commands to avoid accidentally operating under another AWS identity.

## 0.6 Define AWS Regions

The initial AWS region is Asia Pacific (Mumbai).

```text
Region code: ap-south-1
Region name: Asia Pacific (Mumbai)
```

Mumbai provides a consistent starting point for an India-focused application.

### Verify Region Configuration

```powershell
aws configure get region --profile navodayan-dev
```

Expected output:

```text
ap-south-1
```

Before provisioning resources, verify:

- Service availability in the selected region.
- Expected service costs.
- Application latency requirements.
- Applicable data residency requirements.

The region will also be configured in the AWS CDK application during Phase 1.

No additional deployment regions have been configured.

## 0.7 Define Environment Strategy

The platform uses the following environment model:

| Environment | Purpose |
|---|---|
| Local | Development and testing on the developer machine |
| Development | Shared cloud development and integration testing |
| Staging | Pre-production validation |
| Production | Live application workloads |

### Environment Guidelines

- Prefer local development while implementing initial features.
- Keep environment-specific configuration separate.
- Use separate resource names and configuration for each environment.
- Never commit secrets or production credentials.
- Avoid connecting local development to production resources by default.
- Keep production data separate from development and staging data.
- Review deployment changes before applying them.
- Consider separate AWS accounts for stronger isolation as the platform grows.

The initial implementation uses one AWS account. Environment-specific CDK configuration and stacks will be implemented in Phase 1.

## 0.8 Define Infrastructure Naming Convention

Use a consistent naming pattern for AWS resources:

```text
wan-<environment>-<component>-<resource>
```

Where:

- `wan` identifies We Are Navodayan.
- `<environment>` identifies `dev`, `staging`, or `prod`.
- `<component>` identifies the application component.
- `<resource>` identifies the resource type or purpose.

### Naming Examples

```text
wan-dev-network-vpc
wan-dev-backend-cluster
wan-dev-database-postgres
wan-dev-cache-redis
wan-dev-media-bucket
```

These are naming examples only. They do not indicate that the resources have been created.

### Naming Guidelines

- Use lowercase letters and hyphens where supported.
- Include the environment in resource names where practical.
- Follow AWS service-specific naming restrictions.
- Use unique suffixes where required.
- Do not include credentials, secrets, or personal information in names.

The naming convention will be applied through CDK configuration and reusable constructs where appropriate.

## 0.9 Define Resource Tagging Strategy

AWS resource tags help identify project ownership, environments, application components, and cost categories.

The following standard tags will be used where supported:

| Tag | Example | Purpose |
|---|---|---|
| `Project` | `WeAreNavodayan` | Identifies the project |
| `Environment` | `dev` | Identifies the environment |
| `ManagedBy` | `CDK` | Identifies the infrastructure management tool |
| `Owner` | `ProjectTeam` | Identifies resource ownership |
| `Component` | `backend` | Identifies the application component |
| `CostCenter` | `PersonalDevelopment` | Categorizes project costs |

### Tagging Guidelines

- Apply standard tags consistently across supported resources.
- Prefer reusable CDK constructs for applying common tags.
- Do not include credentials or sensitive information in tags.
- Check service-specific tagging limitations.
- Use billing alerts and budget controls in addition to tags.

Tags help categorize costs but do not prevent unexpected charges. Billing controls should be reviewed before significant cloud provisioning.

Automatic tagging through CDK will be implemented during the Infrastructure as Code phase.

## 0.10 Configure Infrastructure Repository Structure

The infrastructure repository is located at:

```text
C:\Users\SanjayKumar6\Desktop\Code\we-are-navodayan\infrastructure
```

The infrastructure directory has its own Git repository on the `main` branch.

The parent `Code` directory also contains a Git repository. It was intentionally left untouched because the web, backend, infrastructure, and shared documentation repositories are maintained separately.

### Initialize Repository

These commands were used during initial setup:

```powershell
$infra = "C:\Users\SanjayKumar6\Desktop\Code\we-are-navodayan\infrastructure"
Set-Location $infra

git init -b main

git config --local user.name "Sanjay Kumar"
git config --local user.email "ersanjay426@gmail.com"
```

### Verify Repository Root

```powershell
git rev-parse --show-toplevel
```

Expected repository root:

```text
C:/Users/SanjayKumar6/Desktop/Code/we-are-navodayan/infrastructure
```

### Verify Branch and Git Identity

```powershell
git branch --show-current
git config --local user.name
git config --local user.email
```

Expected values:

```text
main
Sanjay Kumar
ersanjay426@gmail.com
```

These settings apply only to the infrastructure repository. The global Git identity was not changed.

### Repository Structure

```text
infrastructure/
├── .git/
├── .gitignore
└── README.md
```

The infrastructure-local `docs/` directory was removed. Shared project documentation and cross-repository phase tracking are maintained in the separate `../docs` repository.

### Configure `.gitignore`

The infrastructure `.gitignore` excludes dependencies, CDK output, environment files, private keys, IDE files, logs, and build artifacts.

```gitignore
# Dependencies
node_modules/

# CDK output
cdk.out/

# Environment and secrets
.env
.env.*
!.env.example
*.pem
*.key

# Local IDE and OS files
.vscode/
.idea/
.DS_Store
Thumbs.db

# Logs
*.log

# Build output
dist/
coverage/
```

### Configure README

The root `README.md` describes:

- Infrastructure repository purpose.
- Planned AWS technology.
- Development and security principles.
- Cost-review expectations.
- Reference to the shared `../docs` repository.

### Review and Commit Initial Files

Stage the initial files:

```powershell
Set-Location "C:\Users\SanjayKumar6\Desktop\Code\we-are-navodayan\infrastructure"

git add .gitignore README.md
```

Review the staged changes:

```powershell
git diff --cached
```

Ensure that no credentials, secret values, or unrelated files are included.

Create the initial commit:

```powershell
git commit -m "chore(infra): initialize infrastructure repository for phase 0"
```

Verify the commit and working tree:

```powershell
git log -1 --oneline
git status --short --branch
```

The intended commit message is:

```text
chore(infra): initialize infrastructure repository for phase 0
```

The commit should contain the reviewed `.gitignore` and `README.md` files. Run the verification commands to confirm that the commit exists and the working tree is clean.

---

## Phase 0 Verification

Run the following commands from the infrastructure repository:

```powershell
Set-Location "C:\Users\SanjayKumar6\Desktop\Code\we-are-navodayan\infrastructure"

# Verify AWS CLI installation
aws --version

# Verify configured profiles
aws configure list-profiles

# Inspect profile configuration
aws configure list --profile navodayan-dev

# Verify the configured region
aws configure get region --profile navodayan-dev

# Verify the authenticated AWS identity
aws sts get-caller-identity --profile navodayan-dev

# Verify repository root
git rev-parse --show-toplevel

# Verify branch
git branch --show-current

# Verify latest commit
git log -1 --oneline

# Verify working-tree status
git status --short --branch
```

The AWS identity check must be rerun after replacing the exposed access key. Keep all credentials private.

## Phase 0 Completion Requirements

Before proceeding to CDK bootstrap or deployment:

- Verify AWS CLI authentication using secured credentials.
- Deactivate and replace the exposed access key.
- Review IAM permissions and authentication security.
- Confirm the region, environment strategy, naming convention, and tagging strategy.
- Create and verify the initial Git commit.
- Ensure no credentials or secrets are present in tracked files.
- Review potential AWS costs before provisioning resources.

---

