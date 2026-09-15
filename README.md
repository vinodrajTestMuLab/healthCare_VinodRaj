# Foo Medical — Kane CLI Assurance Demo

A healthcare patient portal demonstration application used to showcase **Kane CLI Assurance**, automated browser testing, evidence generation, and GitHub Actions CI.

> **Important:** Foo Medical is a demonstration application that uses synthetic healthcare information. It is not intended for real patient care or real PHI.

## Application

**Foo Medical:** https://foomedical.com/

Foo Medical provides a patient-portal / EHR-style experience with:

- Patient authentication
- Patient dashboard
- Profile and contact information
- Medical conditions
- Medications
- Allergies
- Laboratory results
- Vital signs
- Appointments
- Appointment scheduling and cancellation
- Patient-provider messaging
- Healthcare documents
- Notifications
- Global search
- Responsive and accessible workflows

## Repository Structure

```text
foo-medical/
│
├── requirements/
│   └── foo-medical-prd.md
│
├── .github/
│   └── workflows/
│       └── foo-medical-kane-assurance.yml
│
└── README.md
```

The repository intentionally starts with only the **product PRD** and **GitHub Actions workflow**.

Kane CLI is responsible for creating and working with the generated test assets during the Assurance workflow.

## Product Context

The product requirements are maintained in:

```text
requirements/foo-medical-prd.md
```

The PRD describes the product itself rather than a test plan. It contains:

- Product overview
- Personas
- Product modules
- User journeys
- Healthcare entities
- Sample synthetic patients
- Providers
- Business rules
- Application behavior
- Error and empty states
- Accessibility expectations
- Responsive behavior
- Healthcare/FHIR concepts

This gives Kane CLI the product context required to understand what Foo Medical is expected to do.

## Kane CLI Assurance Flow

The GitHub Actions workflow follows this lifecycle:

```text
                Foo Medical PRD
                      │
                      ▼
              Context Ingestion
                      │
                      ▼
             Use Case Extraction
                      │
                      ▼
               Test Design
                      │
                      ▼
              Generated Tests
                      │
                      ▼
            Initial Test Authoring
                      │
                      ▼
             Test Suite Execution
                      │
                      ▼
                Evidence Pack
                      │
                      ▼
             Evidence Validation
                      │
                      ▼
                Coverage Report
                      │
                      ▼
             GitHub Actions Artifact
```

The important concept is that the workflow starts with **product requirements** and ends with **execution evidence and assurance coverage**.

## GitHub Actions Workflow

The workflow is:

```text
.github/workflows/foo-medical-kane-assurance.yml
```

It runs on:

- Pull requests
- Pushes to `main`
- Manual `workflow_dispatch`

### Workflow stages

#### 1. Checkout

GitHub checks out the repository.

#### 2. Node.js setup

The workflow uses Node.js 22.

#### 3. Kane CLI installation

```bash
npm install -g @testmuai/kane-cli
```

#### 4. Kane skill installation

```bash
kane-cli install skill
```

#### 5. Authentication

Kane CLI authenticates using GitHub Actions secrets.

#### 6. Product context ingestion

The Foo Medical PRD is supplied to Kane CLI.

```text
requirements/foo-medical-prd.md
```

#### 7. Use-case extraction

Kane CLI extracts product use cases from the PRD.

Examples include:

- Patient login
- Patient dashboard
- Review laboratory results
- Review medications
- Schedule appointment
- Cancel appointment
- Send provider message
- Access documents

#### 8. Test design

Kane CLI designs executable tests from the extracted use cases.

The generated tests cover relevant product behavior rather than requiring the repository to contain hand-written test cases initially.

#### 9. Initial authoring

Generated tests are authored against the Foo Medical application.

```text
https://foomedical.com/
```

#### 10. Assurance execution

The generated tests are executed as a suite.

The workflow uses:

```bash
kane-cli testrun run
```

#### 11. Evidence

Kane CLI generates evidence under:

```text
.testmuai/evidence/
```

#### 12. Evidence validation

The workflow validates generated `.evidence` packs.

A validation failure causes the GitHub Actions job to fail.

#### 13. Coverage

The workflow generates an assurance coverage result with:

```bash
kane-cli cover
```

#### 14. Artifact upload

Evidence, generated tests, coverage information, and supporting artifacts are uploaded to GitHub Actions.

## GitHub Secrets

The workflow expects these repository secrets:

```text
LT_USERNAME
LT_ACCESS_KEY
```

Configure them in:

```text
GitHub Repository
  → Settings
  → Secrets and variables
  → Actions
  → Repository secrets
```

Do **not** commit credentials to the repository.

The workflow references the secrets as:

```yaml
env:
  LT_USERNAME: ${{ secrets.LT_USERNAME }}
  LT_ACCESS_KEY: ${{ secrets.LT_ACCESS_KEY }}
```

## Running the Workflow

### Automatic

Create a pull request or push a commit to:

```text
main
```

GitHub Actions automatically starts the workflow.

### Manual

Go to:

```text
GitHub
  → Actions
  → Foo Medical - Kane CLI Assurance
  → Run workflow
```

## What the Workflow Creates

The repository begins with:

```text
requirements/foo-medical-prd.md
.github/workflows/foo-medical-kane-assurance.yml
README.md
```

During execution, Kane CLI creates/uses additional assets such as:

```text
.context/
.testmuai/
├── tests/
└── evidence/
```

The exact generated files depend on the extracted use cases and execution.

## Evidence

The primary evidence directory is:

```text
.testmuai/evidence/
```

The evidence is used to establish what happened during execution.

The GitHub Actions workflow uploads this evidence as an artifact named:

```text
foo-medical-kane-cli-assurance
```

From the completed workflow run, select:

```text
Summary
  → Artifacts
  → foo-medical-kane-cli-assurance
```

## Assurance Demonstration

A typical demonstration can be presented as:

### 1. Start with the product

Show:

```text
https://foomedical.com/
```

Explain the patient portal and the healthcare workflows.

### 2. Show the PRD

Open:

```text
requirements/foo-medical-prd.md
```

Explain that the product requirements are the source of truth.

### 3. Run GitHub Actions

Open the workflow:

```text
.github/workflows/foo-medical-kane-assurance.yml
```

Show the pipeline progressing through context ingestion, use-case extraction, test generation, authoring, execution, evidence validation, and coverage.

### 4. Show generated tests

Show the generated Kane test assets after the workflow creates them.

### 5. Show execution

Show the workflow executing the healthcare scenarios.

### 6. Show evidence

Download/open the GitHub Actions artifact and show the generated evidence.

### 7. Show coverage

Use the coverage output to explain which product requirements/use cases were exercised and what the execution established.

## Recommended Demo Scenarios

The strongest initial Foo Medical scenarios are:

### Patient Login

```text
Open Foo Medical
    ↓
Enter valid patient credentials
    ↓
Sign in
    ↓
Open Dashboard
    ↓
Verify patient identity
```

### Laboratory Results

```text
Login
    ↓
Open Laboratory Results
    ↓
Search/filter results
    ↓
Open a result
    ↓
Review test name, value, unit and date
```

### Appointment Scheduling

```text
Login
    ↓
Appointments
    ↓
Schedule Appointment
    ↓
Select provider
    ↓
Select appointment type
    ↓
Select date
    ↓
Select available time
    ↓
Confirm
    ↓
Verify appointment
```

### Appointment Cancellation

```text
Upcoming Appointment
    ↓
Open appointment
    ↓
Cancel
    ↓
Confirm
    ↓
Verify Cancelled status
```

### Patient Data Isolation

```text
Login as Patient A
    ↓
Attempt to access Patient B data
    ↓
Verify access is denied
```

This scenario is particularly useful because it demonstrates healthcare-specific authorization behavior rather than only UI navigation.

## Why This Demo

Traditional automation often starts with individual scripts.

This demo starts with the **product definition**:

```text
What should Foo Medical do?
          ↓
Understand the product
          ↓
Identify use cases
          ↓
Create executable tests
          ↓
Run the tests
          ↓
Capture evidence
          ↓
Measure assurance/coverage
```

The value of the demonstration is therefore broader than simply showing that an AI can automate browser actions.

It shows a path from **product intent to executable validation and evidence**.

## Synthetic Data

The demo uses synthetic patients such as:

### Maya Chen

```text
Patient ID: P001
DOB: 1987-04-14
Provider: Dr. Sarah Wilson
```

Example information includes:

- Hypertension
- Seasonal allergic rhinitis
- Migraine history
- Medications
- Penicillin allergy
- Laboratory results
- Vital signs

### Daniel Brooks

```text
Patient ID: P002
DOB: 1979-09-21
Provider: Dr. Michael Lee
```

P002 provides a second synthetic identity for demonstrating patient-specific data separation.

## Prerequisites

Before running the workflow:

1. A GitHub repository containing this project.
2. A valid TestMu AI/LambdaTest username.
3. A valid TestMu AI/LambdaTest access key.
4. The GitHub Actions secrets configured as:
   - `LT_USERNAME`
   - `LT_ACCESS_KEY`
5. Network access from the GitHub Actions runner to the Foo Medical application.

## Troubleshooting

### No tests are generated

Check that the PRD exists at:

```text
requirements/foo-medical-prd.md
```

Also review the context extraction and test-design steps in the Actions log.

### `testrun_plan` contains zero members

This normally means executable test assets were not generated/available before `testrun run`.

Review:

```text
context ingestion
use-case extraction
test design
test generation
```

before investigating the execution step.

### No evidence pack is generated

Check the first failing step before `Validate evidence packs`.

If the test suite did not execute successfully, no final evidence pack may be available.

### Authentication failure

Verify:

```text
LT_USERNAME
LT_ACCESS_KEY
```

exist as GitHub repository secrets and that the values are correct.

## Project Goal

The goal of this repository is to provide a compact, reproducible demonstration of:

**Foo Medical product context + Kane CLI Assurance + GitHub Actions + executable tests + evidence + coverage.**

