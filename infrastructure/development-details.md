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

# Phase 1 — AWS CDK Foundation and Infrastructure as Code

## 1. Phase Overview

**Project:** We Are Navodayan  
**Phase:** 1 — AWS CDK Foundation  
**Status:** Implemented and validated; deployment pending  
**Environment:** Development  
**AWS Region:** `ap-south-1` (Asia Pacific — Mumbai)  
**Infrastructure as Code:** AWS CDK  
**Programming Language:** TypeScript  
**Stack Name:** `we-are-navodayan-dev`  
**Git Branch:** `main`

### Objective

Establish a maintainable infrastructure foundation using AWS CDK and TypeScript. This phase initializes the infrastructure repository, configures the CDK application, creates reusable constructs and environment configuration, defines CloudFormation outputs, validates the application, and verifies the CDK change-review workflow.

**Important:** No application infrastructure resources have been deployed by this phase.

---

## 2. Prerequisites and Tools

The following tools and configurations are available in the development environment.

| Tool | Version observed |
|---|---|
| AWS CLI | 2.38.2 |
| Node.js | 22.18.0 |
| npm | 10.9.3 |
| AWS CDK CLI | 2.1146.0 |
| TypeScript | `~7.0.2` |

Additional prerequisites:

- Git
- AWS account access
- AWS CLI profile named `navodayan-dev`
- AWS region `ap-south-1`
- IAM user `navodayan-dev`
- Existing CDK bootstrap stack

Versions are recorded from the current development environment and may change as dependencies are upgraded.

---

## 3. Repository Structure

The infrastructure repository has been initialized with the following structure:

```text
infrastructure/
├── bin/
│   └── we-are-navodayan-infrastructure.ts
├── lib/
│   ├── config/
│   │   └── environment-config.ts
│   ├── constructs/
│   │   └── project-tags.ts
│   └── we-are-navodayan-infrastructure-stack.ts
├── test/
│   └── we-are-navodayan-infrastructure.test.ts
├── .gitignore
├── README.md
├── cdk.json
├── jest.config.js
├── package.json
├── package-lock.json
└── tsconfig.json
```

### Directory responsibilities

| Path | Responsibility |
|---|---|
| `bin/` | CDK application entry point |
| `lib/config/` | Environment configuration |
| `lib/constructs/` | Reusable infrastructure constructs |
| `lib/` stack file | CloudFormation stack definition |
| `test/` | CDK unit tests |
| `cdk.json` | CDK application command and context |
| `package.json` | Project scripts and dependencies |
| `package-lock.json` | Locked dependency versions |
| `tsconfig.json` | TypeScript compiler configuration |
| `.gitignore` | Excludes dependencies, build output and local secrets |
| `README.md` | Repository overview and usage information |

The infrastructure repository is separate from the web and backend repositories. It uses the `main` branch.

---

## 4. Implementation Details

### 4.1 Install AWS CDK

AWS CDK was installed globally and verified.

```powershell
npm install -g aws-cdk
cdk --version
```

The CDK CLI is available in PowerShell.

### 4.2 Initialize the CDK project

A TypeScript CDK application was generated using the CDK project template.

```powershell
cdk init app --language typescript
```

The generated application files were copied into the existing infrastructure repository while preserving its Git repository and existing documentation.

The project metadata was updated to:

```text
we-are-navodayan-infrastructure
```

Dependencies were installed using:

```powershell
npm install
```

### 4.3 Configure TypeScript

The project includes:

- TypeScript compiler configuration
- CDK application entry point
- Jest test configuration
- AWS CDK dependencies
- TypeScript and testing dependencies

The TypeScript build command is:

```powershell
npm run build
```

The build completed successfully.

### 4.4 Configure CDK project context

The following project-specific values were added to the `context` section of `cdk.json`:

```json
{
  "project": "we-are-navodayan",
  "environment": "dev",
  "awsProfile": "navodayan-dev",
  "awsRegion": "ap-south-1"
}
```

These are the custom context entries, not a replacement for the complete `cdk.json` file. Existing CDK feature flags must remain in place.

The JSON was validated using:

```powershell
node -e "JSON.parse(require('fs').readFileSync('cdk.json','utf8')); console.log('cdk.json is valid JSON')"
```

The configured values were verified as:

```text
project      = we-are-navodayan
environment  = dev
awsProfile   = navodayan-dev
awsRegion    = ap-south-1
```

### 4.5 Configure the CDK application entry point

File:

```text
bin/we-are-navodayan-infrastructure.ts
```

The entry point:

- Creates the CDK application.
- Reads project context.
- Validates required configuration values.
- Resolves the selected environment configuration.
- Creates the infrastructure stack.
- Configures the stack's AWS region and account context.
- Adds project, environment and management tags.

The stack name is:

```text
we-are-navodayan-dev
```

The AWS account is obtained from the CDK CLI environment rather than hardcoded in the application source.

### 4.6 Initialize the infrastructure stack

File:

```text
lib/we-are-navodayan-infrastructure-stack.ts
```

The stack currently defines CloudFormation outputs without defining application infrastructure resources.

This provides a clean starting point for adding networking, compute, databases, storage and other services in subsequent phases.

### 4.7 Create a reusable tagging construct

File:

```text
lib/constructs/project-tags.ts
```

The `ProjectTags` construct applies the following tags:

| Tag | Value |
|---|---|
| `Project` | `we-are-navodayan` |
| `Environment` | `dev` |
| `ManagedBy` | `AWS-CDK` |

The construct is connected to the stack. Actual propagation to application resources has not yet been verified because the current stack contains no application resources.

### 4.8 Add environment configuration

File:

```text
lib/config/environment-config.ts
```

The environment configuration defines:

- Environment name
- AWS region
- Project name
- Removal-policy setting

The current development configuration is:

```typescript
export interface EnvironmentConfig {
  readonly environment: string;
  readonly awsRegion: string;
  readonly project: string;
  readonly removalPolicy: 'retain' | 'destroy';
}

export const environmentConfigs: Record<string, EnvironmentConfig> = {
  dev: {
    environment: 'dev',
    awsRegion: 'ap-south-1',
    project: 'we-are-navodayan',
    removalPolicy: 'destroy',
  },
};
```

**Important:** The `removalPolicy` value is currently configuration only. It is not yet applied to AWS resources. Persistent resources such as databases and uploaded media will require explicit retention safeguards.

### 4.9 Define CloudFormation outputs

The stack defines these outputs:

| Output | Value |
|---|---|
| `ProjectName` | `we-are-navodayan` |
| `EnvironmentName` | `dev` |
| `AwsRegion` | `ap-south-1` |

All three outputs were verified in the synthesized CloudFormation template.

---

## 5. AWS CLI and Bootstrap Configuration

### 5.1 AWS CLI profile

The configured AWS CLI profile is:

```text
navodayan-dev
```

The target AWS region is:

```text
ap-south-1
```

Verify the authenticated identity with:

```powershell
aws sts get-caller-identity --profile navodayan-dev
```

This command succeeded and returned the intended development IAM identity.

### 5.2 Existing CDK bootstrap stack

The AWS account already contains a CDK bootstrap stack.

| Property | Observed value |
|---|---|
| Stack name | `CDKToolkit` |
| Region | `ap-south-1` |
| Status | `CREATE_COMPLETE` |
| Bootstrap version | `32` |
| Qualifier | `hnb659fds` |

The bootstrap stack was already present. It was not recreated during Phase 1.

The bootstrap resources include the CDK asset bucket and roles used for lookup, deployment, file publishing, image publishing and CloudFormation execution.

### 5.3 CDK synthesis

Command:

```powershell
npx cdk synth --profile navodayan-dev
```

**Result: Passed.**

The synthesized template contains:

- Stack description
- CDK bootstrap-version parameter
- `ProjectName` output
- `EnvironmentName` output
- `AwsRegion` output
- CDK metadata

No application infrastructure resources are currently defined.

---

## 6. IAM Permissions and Security

### 6.1 Credential security

During setup, an AWS access key and secret were exposed in the conversation. The exposed key was subsequently deactivated and replaced.

Security requirements:

- Never commit AWS credentials or secrets.
- Never share access key secrets or temporary session credentials.
- Never put AWS credentials in source files or `.env` files committed to Git.
- Do not use root credentials for everyday development.
- Use root only for account-level administration when necessary.

### 6.2 IAM policy configuration

The IAM user `navodayan-dev` initially had no attached permission policies.

The following work was completed:

1. Created and attached the `WeAreNavodayanCDKReadOnly` policy.
2. Added permissions to allow assumption of the relevant CDK roles.
3. Verified assumption of the CDK lookup role.
4. Verified assumption of the CDK deployment role.
5. Verified assumption of the CDK file-publishing role.
6. Inspected the relevant CDK role permissions.
7. Verified that CDK asset publishing and change-set comparison work.

### 6.3 CDK CloudFormation execution role

The CloudFormation execution role currently has a policy that allows:

```json
{
  "Effect": "Allow",
  "Action": "*",
  "Resource": "*"
}
```

This is highly privileged. It should be reviewed as part of the deployment security plan, with the objective of restricting permissions appropriately for the resources that the project actually needs.

Do not grant unrestricted administrator permissions directly to the development IAM user merely to bypass deployment errors.

### 6.4 S3 security

The existing CDK asset bucket has a bucket policy that denies requests when secure transport is not used.

This HTTPS-only protection should remain enabled. Do not make the bucket public or disable S3 public-access protections.

---

## 7. Validation and Test Results

### 7.1 TypeScript build

Command:

```powershell
npm run build
```

**Result: Passed.**

### 7.2 Jest tests

Command:

```powershell
npm test
```

**Result: Passed.**

Observed test summary:

```text
Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
```

**Testing note:** The existing test is still named `SQS Queue Created`, although the current stack does not synthesize an SQS queue. The test should be updated to assert the current stack outputs, description and tags, or replaced with tests appropriate to the actual infrastructure.

### 7.3 CDK synthesis

Command:

```powershell
npx cdk synth --profile navodayan-dev
```

**Result: Passed.**

The synthesized template contains the expected stack description, bootstrap parameter and outputs.

### 7.4 CDK diff

Command:

```powershell
npx cdk diff --profile navodayan-dev
```

**Result: Passed.**

CDK successfully:

1. Built the `we-are-navodayan-dev` template.
2. Published the template to the existing CDK asset bucket.
3. Created a read-only change set to calculate an accurate diff.
4. Displayed the expected stack description, bootstrap parameter and outputs.

The diff reported one stack with differences.

The reported differences were limited to the stack description, bootstrap-version parameter and the three CloudFormation outputs.

No application infrastructure deployment was performed.

---

## 8. Git History and Commit

The infrastructure repository contains these commits:

```text
58afa3c Phase 1 : Initialize AWS CDK infrastructure
2206854 Phase 0 : Infrastructure & Cloud Foundation
```

The Phase 1 commit includes:

- CDK application entry point
- CDK configuration
- Environment configuration
- Reusable tagging construct
- Infrastructure stack
- Jest test configuration and test file
- TypeScript configuration
- Package metadata and lockfile

After the commit, the following validation commands were executed:

```powershell
git status --short --branch
npm run build
npm test
npx cdk synth --profile navodayan-dev
```

The Git status was clean on branch `main`, and the build, test suite and synthesis succeeded.

---

## 9. Phase 1 Completion Checklist

- [x] Install AWS CDK.
- [x] Initialize the TypeScript CDK project.
- [x] Configure project metadata.
- [x] Configure project context.
- [x] Create the CDK application entry point.
- [x] Initialize the infrastructure stack.
- [x] Create reusable project-tagging construct.
- [x] Add environment configuration.
- [x] Define CloudFormation outputs.
- [x] Verify AWS CLI profile and identity.
- [x] Verify existing CDK bootstrap stack.
- [x] Run TypeScript build.
- [x] Run existing Jest test suite.
- [x] Run CDK synthesis.
- [x] Run CDK diff successfully.
- [x] Commit Phase 1 changes.
- [x] Verify a clean Git working tree.
- [ ] Align tests with the current stack implementation.
- [ ] Review least-privilege deployment permissions.
- [ ] Verify resource tagging when actual resources are added.
- [ ] Review costs and security controls before deploying infrastructure.
- [ ] Deploy the first application infrastructure resource.

### Overall status

**Phase 1 foundation: Implemented and validated.**

**AWS application infrastructure deployment: Pending.**

The infrastructure repository is ready for the next implementation phase, subject to the remaining test-alignment and deployment-security reviews.

---
