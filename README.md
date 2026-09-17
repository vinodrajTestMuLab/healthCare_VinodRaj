# Foo Medical — KaneCLI Login Assurance Demo

A minimal Foo Medical demonstration showing how **TestMu AI KaneCLI** can turn a product requirement into an executable browser test and produce Assurance evidence.

## Demo Flow

```text
PRD
 ↓
Use Case
 ↓
Acceptance Criterion
 ↓
Generated Test
 ↓
Browser Execution
 ↓
Evidence
 ↓
Coverage
```

## What This Demo Tests

Only one workflow is in scope:

**Open Foo Medical → Sign in with valid patient credentials → Verify the patient dashboard is visible**

The goal is to demonstrate the KaneCLI Assurance lifecycle with the smallest practical example.

## Files

```text
.
├── requirements/
│   └── foo-medical-prd.md
│
├── .github/
│   └── workflows/
│       └── foo-medical-kane-assurance.yml
│
├── .testmuai/
│   ├── tests/
│   └── evidence/
│
├── .artifacts/
│
└── README.md
```

### Source of Truth

`requirements/foo-medical-prd.md` is the product requirement used by KaneCLI.

It intentionally contains only one use case and one acceptance criterion.

### Generated Tests

KaneCLI generates the browser test under:

`.testmuai/tests/`

The first run authors the generated test in a real browser. Subsequent runs can replay the recorded test.

### Evidence

After a successful run, KaneCLI creates a sealed `.evidence` pack under:

`.testmuai/evidence/`

The workflow validates the pack and uploads it as a GitHub Actions artifact.

### Coverage

The workflow exports coverage to:

`.artifacts/coverage.json`

This is generated after successful execution.

## GitHub Secrets

Configure these repository secrets before running the workflow:

```text
LT_USERNAME
LT_ACCESS_KEY
FOO_MEDICAL_EMAIL
FOO_MEDICAL_PASSWORD
```

The Foo Medical credentials are supplied only at runtime and are not stored in the repository.

## Run the Demo

The workflow is manual-only.

In GitHub:

**Actions → Foo Medical - KaneCLI Assurance → Run workflow**

The workflow then:

1. Installs KaneCLI.
2. Logs in to TestMu AI.
3. Ingests the PRD.
4. Extracts the use case.
5. Designs one browser test.
6. Supplies the patient credentials securely.
7. Authors and executes the test.
8. Validates the evidence pack.
9. Calculates coverage.
10. Uploads the generated outputs.

## Application Under Test

Foo Medical:

https://foomedical.com/

Foo Medical is an open-source healthcare sample application from the Medplum team.

## Why This Demo Is Small

This repository is designed to show the Assurance concept without introducing unnecessary test data or workflow complexity.

The demo intentionally excludes appointments, messaging, medications, laboratory workflows, registration, API testing, backend testing, and multi-patient scenarios.

## Core Message

The demonstration is not simply about generating a browser test.

It shows the chain:

**What should the product do? → What should be verified? → Did it work? → Where is the evidence?**

## Upstream Project

Foo Medical:

https://github.com/medplum/foomedical

Medplum:

https://www.medplum.com/
