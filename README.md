# Windows Master

Windows Master is a long-term engineering platform for secure, repeatable, and
auditable Windows administration. It is intended to bring automation, policy,
recovery, observability, and bounded AI-assisted operations into one governed
repository.

> **Project status:** Foundation stage. Repository governance and development
> scaffolding are present; production automation components have not yet been
> implemented.

## Project Vision

Windows Master aims to provide a trusted control plane for managing Windows
environments across workstations, servers, laboratories, and enterprise estates.
The platform should make administrative intent explicit, validate current state
before acting, require approval where risk demands it, and retain evidence that
the desired state was achieved.

The long-term outcome is an operational system in which:

- routine changes are declarative, idempotent, testable, and reversible;
- privileged actions use least privilege and narrowly scoped approvals;
- configuration, inventory, execution, and verification are separate stages;
- recovery procedures are designed and tested with the corresponding changes;
- every material operation produces sanitized, structured audit evidence; and
- AI agents assist within defined roles without becoming an authority boundary.

## Mission and Enterprise Objectives

The project exists to improve Windows operational reliability without weakening
security, recoverability, or supportability. Its enterprise objectives are to:

- standardize Windows administration across teams and environments;
- reduce interactive, workstation-specific, and undocumented procedures;
- provide reusable automation with predictable failure behavior;
- integrate security controls and approval gates into normal workflows;
- support compliance evidence without collecting unnecessary sensitive data;
- enable safe extension through projects, templates, agents, and integrations;
- measure operational outcomes and continuously improve them; and
- preserve compatibility with documented Microsoft management interfaces.

## Design and Operating Principles

Priorities are applied in this order:

1. Safety
2. Correctness
3. Recoverability
4. Maintainability
5. Reproducibility
6. Performance

Automation should prefer supported platform APIs, PowerShell cmdlets, CIM, DISM,
documented Microsoft APIs, declarative configuration, and explicit state
verification. A successful command is not sufficient evidence of a successful
change.

The repository-wide engineering and security requirements are defined in
[AGENTS.md](AGENTS.md). More specific instructions may be added within individual
projects, but they must not weaken the root policy.

## Current Progress

| Area | State | Evidence |
| --- | --- | --- |
| Repository governance | Established | Root `AGENTS.md` defines safety, approval, security, testing, and operational policies |
| Repository layout | Established | Standard directories exist for projects, scripts, configuration, documentation, agents, templates, logs, backups, and experiments |
| Source-control hygiene | Established | Root `.gitignore` covers secrets, local environments, caches, generated output, and runtime artifacts |
| Editor integration | Initial | Portable VS Code settings, tasks, launch configurations, and extension recommendations are present |
| Validation workflow | Initial | VS Code tasks are configured for PowerShell syntax, PSScriptAnalyzer, Ruff, and pytest |
| Production automation | Not started | No production scripts, modules, or applications are present |
| Automated test suites | Not started | No project test suites or fixtures are present |
| CI/CD and release process | Not started | No pipeline, artifact publication, or release policy is implemented |
| Enterprise integrations | Planned | Identity, endpoint management, ticketing, secret-store, and observability integrations remain future work |

Status descriptions reflect repository evidence, not planned capability.

## Project Roadmap

The roadmap is organized by capability maturity. It deliberately avoids delivery
dates until ownership, scope, dependencies, and capacity are established.

### Phase 1: Foundation

- Finalize repository governance, ownership, support, and licensing.
- Define supported Windows editions, PowerShell versions, Python versions, and
  execution environments.
- Establish formatting, linting, unit testing, secret scanning, and CI checks.
- Add project templates, Architecture Decision Record templates, and runbook
  templates.
- Define artifact signing, provenance, dependency, and release policies.

**Exit criteria:** documented ownership and support boundaries, reproducible
development setup, enforced quality gates, and a reviewed reference project.

### Phase 2: Core Automation

- Build inventory and state-discovery libraries.
- Establish configuration models and validation schemas.
- Implement safe execution primitives with `-WhatIf`, approval, timeout,
  cancellation, retry, rollback, and verification support.
- Add structured logging, correlation identifiers, and redaction controls.
- Deliver initial runbooks and isolated integration tests.

**Exit criteria:** core operations are idempotent, observable, tested in disposable
Windows environments, and recoverable under documented failure scenarios.

### Phase 3: Governance and Security

- Integrate approved secret stores and identity providers.
- Add policy evaluation, role-based authorization, and separation of duties.
- Implement signed artifacts, software bills of materials, provenance evidence,
  and controlled promotion between environments.
- Add compliance mapping, exception lifecycles, and audit reporting.

**Exit criteria:** privileged operations are attributable, policy-controlled,
reviewable, and supported by retained audit evidence.

### Phase 4: Enterprise Integration

- Integrate endpoint management, directory services, ticketing, monitoring,
  backup, and configuration platforms through approved adapters.
- Add bounded orchestration across hosts and environments.
- Define maintenance windows, concurrency limits, health gates, and failure-domain
  controls.
- Introduce AI-assisted planning and analysis behind the same approval and policy
  boundaries as human-initiated operations.

**Exit criteria:** integrations have documented owners, versions, data flows,
authentication, timeouts, rollback behavior, and operational support procedures.

### Phase 5: Operational Maturity

- Define service-level indicators, objectives, and error budgets.
- Measure recovery time, recovery point, change failure rate, and automation
  effectiveness.
- Exercise disaster recovery and degraded-operation procedures.
- Establish lifecycle management, deprecation, migration, and periodic control
  review.

**Exit criteria:** the platform has measurable reliability, tested recovery,
maintained operational ownership, and evidence-driven improvement processes.

## Target AI Architecture

AI is a governed assistance layer, not a security principal or source of truth.
Agents operate with narrow roles, explicit inputs and outputs, bounded tools,
clear termination conditions, and evidence-based verification.

```text
Request or approved event
          |
          v
Coordinating agent
  - scope and target resolution
  - risk classification
  - approval ownership
  - conflict resolution
          |
          v
Specialized bounded agents
  - discovery        - planning
  - implementation   - validation
  - documentation    - recovery analysis
          |
          v
Policy and approval boundary
  - identity and authorization
  - target and input validation
  - secret and data controls
  - change-window and risk gates
          |
          v
Approved adapters and execution services
  - Windows management APIs
  - configuration and endpoint platforms
  - secret stores, MCP servers, and enterprise integrations
          |
          v
Independent verification and audit evidence
```

The coordinating agent owns scope, approvals, conflict resolution, and final
verification. Delegated agents cannot expand authority or delegate permissions
they were not granted. Agent confidence is never treated as evidence; resulting
state must be checked through authoritative interfaces.

MCP servers and other tool integrations require documented ownership, pinned
versions where possible, explicit data-flow review, minimum required permissions,
timeouts, and failure behavior. Their output is treated as untrusted input.

## Repository Structure

| Path | Purpose |
| --- | --- |
| `Projects/` | Independently maintained applications and automation packages |
| `Scripts/` | Shared PowerShell and Python operational tooling |
| `Config/` | Versioned, non-secret configuration and configuration examples |
| `Templates/` | Reusable scripts, documents, runbooks, and project scaffolds |
| `Documents/` | Architecture decisions, specifications, runbooks, and recovery procedures |
| `Agents/` | AI agent definitions, prompts, policies, and supporting resources |
| `Sandbox/` | Isolated experiments; production workflows must not depend on it |
| `Backups/` | Approved local backup artifacts or backup manifests |
| `Logs/` | Sanitized, bounded runtime logs suitable for repository storage |
| `.vscode/` | Portable workspace settings, tasks, launch configurations, and extension recommendations |

Each maintained project should contain its own `README.md`, source, tests,
configuration examples, dependency lock files, ownership information, and support
status. Generated output belongs outside source directories.

## Future Components

The following components describe intended capability domains, not implemented
features:

| Component | Intended responsibility |
| --- | --- |
| Inventory and discovery | Collect normalized hardware, software, service, feature, policy, and configuration state |
| Configuration management | Model desired state, detect drift, plan changes, apply safely, and verify convergence |
| Compliance assessment | Evaluate approved controls, retain evidence, track exceptions, and produce sanitized reports |
| Patch orchestration | Assess applicability, stage changes, enforce maintenance windows, verify health, and support rollback |
| Identity and access integration | Apply least privilege, role-based access, managed identity, and separation of duties |
| Backup and recovery | Coordinate protected backups, integrity checks, restore tests, and recovery evidence |
| Monitoring and reporting | Emit structured telemetry, operational health, trends, and actionable failure context |
| Package and artifact service | Build, sign, attest, scan, retain, and promote trusted automation artifacts |
| Policy and approval service | Classify risk and enforce authorization, approval, scope, and expiration rules |
| Orchestration engine | Coordinate bounded execution with concurrency, timeout, cancellation, and failure-domain controls |
| Integration adapters | Connect approved Microsoft and enterprise systems through versioned, testable interfaces |
| Agent runtime | Execute bounded AI workflows with policy enforcement, tool restrictions, and complete audit trails |
| Operator interface | Present plans, risk, approvals, progress, evidence, rollback, and escalation guidance |

Architecture decisions for consequential components should be recorded as
Architecture Decision Records under `Documents/`.

## Prerequisites and Supported Environments

No production support matrix has been approved. Every project must declare:

- supported Windows editions, versions, architectures, and patch levels;
- required PowerShell edition and minimum version;
- required Python version and isolated-environment setup, when applicable;
- dependencies, pinned versions, provenance, and installation method;
- required privileges and external services;
- network, maintenance-window, and restart implications; and
- the environment used for integration and recovery testing.

The current workspace assumes Git and optionally Visual Studio Code. Configured
validation tasks also expect the relevant tools to be installed:

- Windows PowerShell for syntax validation and task execution;
- PSScriptAnalyzer for PowerShell analysis;
- Python with Ruff for Python linting; and
- Python with pytest for Python tests.

These tools are development scaffolding, not a declared production runtime.

## Getting Started

1. Clone the repository using the approved organizational Git workflow.
2. Read [AGENTS.md](AGENTS.md) before making changes.
3. Review `git status` and confirm that the working tree contains no unrelated
   changes.
4. Open the repository root in Visual Studio Code if using the provided workspace
   configuration.
5. Install only the dependencies required by the project being changed, using its
   documented and pinned setup process.
6. Perform administrative integration tests only in a disposable VM, Windows
   Sandbox, or another approved isolated host.

Do not execute repository content against production systems by default. A
project's runbook must identify its target, prerequisites, privileges, risks,
approval requirements, rollback, and verification procedure.

## Configuration and Secret Management

Only non-secret configuration and sanitized examples belong in Git. Store
passwords, tokens, private keys, certificates, recovery keys, and production
connection strings in Windows Credential Manager, an approved secret store,
managed identity, or protected CI/CD variables.

Configuration loaders should:

- validate and canonicalize all user-controlled values;
- reject missing authorization or invalid targets;
- separate defaults, environment-specific values, and secrets;
- avoid logging sensitive values or command-line arguments; and
- provide actionable failures without exposing protected data.

The `.gitignore` reduces accidental inclusion but is not a security control.
Review staged changes and run approved secret scanning before every commit.

## Development and Change Workflow

Use a staged workflow:

1. **Discover:** inspect current state and validate target identity.
2. **Plan:** define desired state, affected scope, prerequisites, risk, and
   maintenance requirements.
3. **Protect:** establish backup or recovery measures appropriate to the risk.
4. **Approve:** obtain operation-specific approval immediately before privileged,
   destructive, externally visible, billable, or downtime-capable actions.
5. **Execute:** make the smallest supported change with bounded privileges.
6. **Verify:** independently confirm resulting state and operational health.
7. **Record:** retain sanitized evidence, decisions, rollback data, and outcomes.

Mutating PowerShell advanced functions should support `SupportsShouldProcess`,
`-WhatIf`, and `-Confirm`. Retries must be bounded and limited to transient
failures; authorization, validation, and deterministic errors must not be retried.

## Testing and Validation

Tests should cover normal, failure, boundary, permission-denied, timeout, and
rollback paths. They must be independent, reproducible, and limited to resources
they create.

The VS Code task **Validate: Workspace** runs the configured checks in sequence:

1. PowerShell syntax validation
2. PSScriptAnalyzer
3. Ruff
4. pytest

Projects may add stricter checks. Before committing, review the complete diff and
run all relevant formatters, linters, tests, security checks, and isolated
integration tests. Document commands and sanitized results in the change or pull
request.

## Security and Approval Model

Explicit approval is required immediately before any operation that is:

- destructive or difficult to reverse;
- privileged;
- externally visible or billable;
- capable of causing downtime; or
- able to alter security, access, identity, recovery, or trust controls.

Approval must identify the exact target, expected effect, risk, rollback or backup
path, and verification method. Earlier approval does not authorize broader scope.
Security controls must not be disabled to make automation pass.

Suspected credential exposure or unauthorized access requires immediate
containment of related automation, preservation of relevant evidence, and
escalation through the approved incident process.

## Logging, Audit, Backup, and Recovery

Operational logs should be structured and include UTC timestamp, severity,
operation or correlation identifier, component, target, outcome, duration, and
actionable error context. Redact sensitive data at the source and enforce bounded
retention so logs cannot exhaust storage.

High-risk changes require a recovery plan before execution. Backup procedures must
define scope, destination, encryption, retention, owner, integrity verification,
and restoration steps. Critical backups require a documented restore test. Never
delete the only known-good copy.

Repository `Logs/` and `Backups/` content must be sanitized and explicitly
approved for version control. Sensitive or high-volume operational data belongs
in approved external systems.

## Project Package Standards

Each package under `Projects/` should provide:

- purpose, scope, owner, support status, and lifecycle state;
- prerequisites and a supported-environment matrix;
- versioned source and configuration examples;
- pinned runtime and development dependencies;
- unit and isolated integration tests;
- usage, troubleshooting, and escalation guidance;
- security and data-flow documentation;
- exact prechecks, execution, expected output, and verification steps;
- rollback and recovery instructions; and
- release notes or another traceable change record.

Interfaces shared across projects should be promoted into `Scripts/`, `Templates/`,
or a dedicated common package only after their ownership and compatibility policy
are defined.

## Contribution and Git Conventions

Use focused branches such as:

- `feature/inventory-export`
- `fix/service-timeout`
- `docs/recovery-runbook`

Use imperative Conventional Commit messages, for example:

```text
fix: preserve ACLs during backup
```

Pull requests should include purpose, risk assessment, test evidence, operational
impact, rollback guidance, and a linked work item when available. Security-
sensitive or administrative code requires review. Do not rewrite shared history,
bypass branch protection, force-push, or merge failing checks without explicit
authorization.

## Support, Ownership, and Lifecycle

Formal ownership, support channels, service levels, and release cadence have not
yet been assigned. Until they are documented, Windows Master should be treated as
an engineering foundation rather than a supported production service.

Every production-capable component must identify:

- accountable owner and maintainers;
- supported versions and environments;
- issue, incident, and security escalation paths;
- release, maintenance, and deprecation policy; and
- recovery and continuity responsibilities.

## License

No license has been declared. Do not assume permission to use, redistribute,
modify, or publish this repository outside the authorization granted by its
owner. Add an approved `LICENSE` file before external distribution.
