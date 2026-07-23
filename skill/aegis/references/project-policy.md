# Project Policy and Delegation

Use this reference when configuring Aegis for a project. It defines the project-local policy boundary, who may make decisions, and the minimum quality controls. It does not replace a project's approved specification, build package, or gate record.

## AI SDLC Policy in `AGENTS.md`

`AGENTS.md` is the canonical per-project configuration surface. Aegis policy must live in one clearly delimited `AI SDLC Policy` section so the policy can be found, reviewed, and changed without rewriting a project's other instructions.

Use stable start and end markers around the section, for example:

```md
<!-- AEGIS AI SDLC POLICY: START -->
## AI SDLC Policy

### Project Configuration
- Risk classification: `standard`
- PM / HITL: `<role or name>`
- Artifact location: `<path>`
- Approved model mapping: `<mapping or see Roles and Models>`
- Gate policy: `<risk-scaled gate policy>`

### Required Controls
- Preserve durable project artifacts and record approvals in `journal.md`.
- Route delivery-agent questions through the PM to the HITL.
- Stop at every required approval gate.
<!-- AEGIS AI SDLC POLICY: END -->
```

When adding or changing this section:

1. Read the whole existing `AGENTS.md` and the current project artifacts.
2. If the delimited section exists, update only its contents and preserve all material outside the markers exactly.
3. If it does not exist, append the complete delimited section without rewriting unrelated instructions.
4. Record the policy decision and any material change in `journal.md`.
5. If a policy change affects approved scope, architecture, risk, evidence, or gates, pause, update the affected artifacts, reclassify risk when needed, and repeat the invalidated review and approval gates. High/critical material decisions require an ADR.

Never overwrite an existing lifecycle artifact merely to make it fit a template. Preservation is the default; a deliberate, approved change is the exception.

## Conflict Is a Hard Stop

When project instructions, `AGENTS.md`, code, contracts, tests, approved artifacts, evidence, or the AI SDLC Policy conflict, stop work. Surface the specific conflict, the affected decision or task, and the evidence on each side. The PM must obtain an explicit HITL resolution and record it before work continues.

Do not silently choose a precedence rule, infer that newer prose wins, or let a delivery agent resolve the conflict locally. Security red lines remain non-negotiable: no secret exposure, unsafe credential handling, or quietly accepted dangerous pattern is made permissible by a conflict decision.

## PM, HITL, and Delivery Roles

The initiating agent is the non-implementing product manager (PM) and acts as the Principal Engineer responsible for product and project management. The PM:

- owns and maintains `README.md`, `journal.md`, `status.md`, `spec.md`, and `build-package.md`;
- reconstructs context from project artifacts before chat history and records decisions, approvals, evidence, risks, and open loops durably;
- decomposes approved requirements into bounded, dependency-aware work items with an owner role, model, prerequisites, deliverable, verification, and entry and exit criteria;
- supervises delivery, checks requirements and phase criteria, and independently reviews bounded subagent output; and
- is the only route between delivery agents and the human in the loop (HITL).

Delivery agents ask the PM one focused question at a time. The PM decides whether the question requires HITL input, then presents one focused decision with numbered options and a recommendation when tradeoffs matter. A delivery agent does not ask the HITL directly, grant itself a gate approval, or expand its assigned boundary.

Use roles according to the work, not as decorative titles:

| Role | Accountable work |
| --- | --- |
| PM / Principal Engineer | Lifecycle artifacts, risk and dependency control, delegation, reviews, and HITL routing. Does not implement product changes. |
| Coder | Bounded product changes, scaffolding, and approved promotion mechanics. |
| Tester | Independent structural, automated, regression, and forward verification. |
| SecOps | Proportional security review, threat and permission analysis, and security evidence. |
| Documentation | Product, operational, and reference documentation. The PM retains lifecycle-artifact ownership. |

For trivial or small work, use zero or one subagent when that is enough. For a larger project, staff three or more bounded agents as needed; multiple agents may share a role. The PM chooses multimodal delegation in this order: cost, accuracy, then speed.

## Models and Fallbacks

Use the approved model profile when available:

| Work | Default model |
| --- | --- |
| Design, planning, documentation, substantial review | GPT-5.6 Terra medium or high |
| Coding, testing, and mechanical work without substantial reasoning | GPT-5.6 Luna-low |
| Escalation | GPT-5.6 Sol only with explicit HITL permission |

If a named model is unavailable, do not silently substitute a weaker or more expensive model. The PM asks the HITL to approve an available model with an equivalent reasoning or execution capability for the affected role. Record the mapping and its rationale in the durable project record.

## Testing, SecOps, and Reviews

Every project requires testing. The PM may perform and record validation only for trivial work. Standard, high/critical, and public-facing projects require independent testing.

Require a SecOps reviewer for every standard or high/critical project and for any public-facing application or service. Security validation is mandatory before commit or deployment. A proof of concept may relax peripheral controls only with explicit risk treatment; it may not relax foundational security hygiene.

Both pre-code and post-implementation reviews must explicitly assess:

- security;
- best practices;
- maintainability;
- observability;
- monitoring when the system is long-running; and
- documentation.

For each dimension, record the finding, evidence, applicability, and outcome: fixed, accepted as a documented risk, or escalated to the HITL. A statement that monitoring is not applicable must explain why; it is not a blank checkbox.

## Strict Gates

Scale ceremony to risk, reversibility, and blast radius. Classify work as `trivial`, `low`, `standard`, or `high/critical`; security/authentication, secrets, personal or customer data, production infrastructure, payments, destructive migration, and public release work are automatically `high/critical`.

- **Trivial:** record scope, verification, and closeout.
- **Low:** require scope and acceptance approval.
- **Standard:** require build-package, pre-code review, execution, acceptance, commit, and applicable release approvals.
- **High/critical:** require all nine gates.

At every required human approval gate, stop and wait. Present the decision as: `1. Approve`, `2. Revise`, or `3. Stop/Defer`, then record the choice and its evidence. A genuinely inapplicable gate remains visible in `status.md` as `Not applicable` with its rationale and closeout evidence.

The non-negotiable blocking points are:

| Gate | Required decision before proceeding |
| --- | --- |
| G1 | Scope approval before the approved work is treated as the project boundary. |
| G2 | Build-package approval before pre-code work is treated as code-ready. |
| G3 | Pre-code review approval before execution can be requested. |
| G4 | Explicit HITL execution authorization before any coding or product change begins. |
| G5 | Manual acceptance of finished source before commit or release decisions. |
| G6 | Explicit commit authorization where version control is used. |
| G7 | Explicit deployment authorization before package/runtime promotion or other deployment. |
| G8 | Explicit post-deployment acceptance after installed/released verification. |
| G9 | Explicit push/PR/closeout authorization after durable records are complete. |

No agent may provisionally cross a hard gate. Material approved changes reopen the affected risk assessment, reviews, and gates; they do not inherit approval from the earlier version.
