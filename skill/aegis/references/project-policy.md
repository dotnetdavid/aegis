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
- Development approver: `<owner by default; explicit bounded delegation/source if any>`
- Delegation bounds: `<scope, acceptance, exclusions, timebox, reserved decisions>`

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

## Master-Specification Authority

The project-root `spec.md` is the one current product requirements and
architecture authority. Current code, schemas, tests and observed results
establish existing behavior, not authority to change what is required. The AI
SDLC Policy, `AGENTS.md`, backlog, chat, scope record, build package, review,
receipt and other history cannot override approved product requirements. Apply
the lifecycle bootstrap rule for the first and only master spec; never create
a replacement or parallel specification.

Every governed run validates the current master spec before planning and writes
a new immutable package bound to its spec identity and covered requirement IDs;
the one compact brief serves as the package on the eligible trivial/low path.
If a request lacks a spec, carries unsafe metadata, names missing/stale/unknown/
duplicate/retired IDs, attempts sidecar authority, or changes final spec text
without an approved mapping, stop and route one focused resolution question to
the HITL. Maintain append-only authority/inventory evidence; preserve prior
records as non-authoritative history.

## Development Approver

Use the Development Authority definition in SKILL.md: the owner/HITL by default,
or an explicitly delegated PM for named bounded isolated development decisions.
A project profile records authority; it does not create it. Owner-reserved decisions,
production promotion and platform confirmations cannot be inferred away.

## PM, HITL, and Delivery Roles

The initiating agent is the non-implementing product manager (PM) and acts as the Principal Engineer responsible for product and project management. The PM:

- owns the master spec, preserves existing records, and maintains standard/high
  `README.md`, `journal.md`, `status.md`, and `build-package.md`, or the compact
  brief and one existing linked ledger for eligible trivial/low;
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

For eligible lightweight delivery, explicitly name the human implementer
(no delivery subagent) or one bounded delivery agent in the run brief. If
neither is available, hold implementation. The PM remains non-implementing
and reviews the full actual diff. Owner/PM validation on this path is not
independent verification.

Staff other roles as required by risk and evidence. Choose bounded delegation by cost, accuracy, then speed.

## Run Budget

Before running any actual check, starting product work or dispatching it
(including delegated checks/reviews), verify the authorized run budget.
Record the run identity, observed elapsed start and deadline or limit,
per-item and run-wide attempt/retry limits, and any applicable usage/spend
and concurrency ceilings. Name the authoritative counter/clock and
observable usage source, units and measurement frequency; record applicable
paid usage only with explicit authority. An owner-approved profile may supply
bounds within its scope. A missing bound or untrackable applicable capacity
is a hold, not permission to use an uncapped default.

The PM owns one shared budget ledger across agents, sessions, roles and
routes. Count an initial attempt when it starts and every retry as another
attempt against both its item and the run totals. Repeating failed or blocked
work, rerunning an attempted check, reviewing a corrected candidate, or having
a replacement agent repeat work counts even across reboot/session or identity
change. A distinct check step already planned in the frozen contract is not
a retry merely because it follows another check (for example, the planned
pre-edit and post-edit runs of the same unchanged check); it still consumes
applicable time, usage and capacity. No-progress/cosmetic/unchanged candidates and
relabeled blockers stop regardless of remaining budget.

Reserve capacity in the shared ledger before parallel dispatch; do not count
one slot twice or admit work that cannot fit the remaining time, attempt,
usage, or concurrency bounds. Reconcile reservations with observed consumption
and release only verified unused capacity. While work is active, recheck
capacity using the recorded sources. If a limit is reached or accounting is
lost, start no new work or retry. Safely pause, cancel, or drain affected
in-flight work only through authorized controls, record what actually stopped
or remains active and what could not be accounted for, then hold.

Continue only with an explicit bounded extension from the authorized decision
maker, linked to the existing run and receipts. Record affected item/scope,
added capacity, deadline and observable accounting; retain elapsed and
attempt/usage history and reservations. Replacement, reboot, a new route or
renaming the run does not restore capacity. Do not infer spending, a third
review cycle, or other reserved authority from a budget extension. Use host
limits where available; documented rules are not proof of runtime enforcement.

## Models and Fallbacks

Use a project-approved mapping of available models: sufficient reasoning for
substantive engineering/review and lowest-cost adequate capability for mechanical
work. An unavailable choice requires owner approval or a PM mapping within explicit
owner delegation. Record mapping and rationale, actual routing when exposed or
unknown when not. Never silently change capability or add spending.

## Testing, SecOps, and Reviews

Independent PE and SecOps may use separate sections in a shared append-only
review record. Each actual author records role, date, candidate identity, evidence
and disposition; preserve findings and prior decisions. No PM-authored proxy
approvals: sharing storage does not substitute for independent judgment.

Every project requires testing. The owner/PM may perform and record validation for eligible trivial or low-risk work. Standard, high/critical, and public-facing projects require independent testing.

Require a SecOps reviewer for every standard or high/critical project and for any public-facing application or service. Security validation is mandatory before commit or deployment. A proof of concept may relax peripheral controls only with explicit risk treatment; it may not relax foundational security hygiene.

Both pre-code and post-implementation reviews must explicitly assess:

- security;
- best practices;
- maintainability;
- observability;
- monitoring when the system is long-running; and
- documentation.

For each dimension, record the finding, evidence, applicability, and outcome: fixed, accepted as a documented risk, or escalated to the HITL. A statement that monitoring is not applicable must explain why; it is not a blank checkbox.

### PII Check and Privacy Stop

Every SecOps review includes a proportional PII check of the authorized affected
codebase and artifacts. Record scope, methods and material limitations. A user may
request a bounded check; that request does not grant gate authority. Ordinary
authorized data presence is not itself a leak. Assess actual unauthorized exposure,
disclosure or mishandling; do not presume safety merely because use is internal.

An evidence-backed suspected leak pauses affected work. Complete safe evidence
gathering within the authorized scope without continuing the suspected exposure.
Record a stable finding ID, repository-relative file/line, uncertainty, unresolved
state and impact-based severity with its evidence; severity is not automatically P0.
Do not reproduce the suspected value or source snippet. Only the owner/HITL may
record disposition: direct correction/removal or approve a documented exemption,
subject to platform rules. Keep affected work paused until its findings have owner
disposition. Independent unaffected authorized work may continue if safe. Clearing
a privacy pause does not approve, bypass, advance or reopen a gate.

If the authorized check cannot be completed, record `scan incomplete` and the
scope/limitations; affected work remains paused until completed or the owner
changes scope through normal control. A clean result records its scope, methods
and limitations, not a certification that no PII exists.

## Contract-First Work Items

Contract-first control applies to every product-changing work item: code,
configuration, infrastructure, documentation, templates, and skill guidance.
Executable work uses a test contract; non-executable work uses an
artifact-appropriate validation contract.

For eligible trivial or low-risk work, the owner/PM prepares a concise brief and minimal
contract/validation plan, checks adequacy, obtains explicit scope/acceptance
authorization and records G4 as not applicable with rationale. The owner/PM may
create, review and run the checks. For standard, high/critical and public-facing
work, prepare the contract and check design before applicable G4; the development
approver must authorize G4 before actual checks or product artifacts. After G4,
the tester creates actual checks and independent PE approves adequacy.

For executable items, select and record the expected pre-edit result in the
approved contract. New behavior and bug fixes require observable RED for the
intended reason before product work, then GREEN after the edit with the unchanged
approved checks. A behavior-preserving refactor may use GREEN -> GREEN only when
the approved contract documents the behavior and acceptance criteria that must
remain unchanged. The approved checks must all pass before product work and
pass unchanged after the edit. A failing baseline blocks this path; do not
manufacture RED, waive a failure, or change the checks to obtain GREEN. Separate
any new behavior or fix into its own RED -> GREEN item with its own evidence.
Classifying an item does not change applicable authorization, tester
independence, adequacy review, scope review, or acceptance requirements.
For non-executable work, use and record justified artifact-appropriate validation.
Retain results and inspect evidence; authorization does not waive validation.

Each contract records, at minimum:

- unique work-item ID, contract ID, revision, and lineage;
- exact master-spec requirement and acceptance criteria;
- artifact kind and purpose;
- inputs, expected behavior or output, and the assertion/oracle or validation
  criteria;
- positive, negative, and edge cases;
- direct dependencies, downstream dependents, and the rebuild boundary;
- relevant permissions, security, and privacy constraints; and
- expected check outcomes and applicable approval requirements.

Freeze the plan and contract by identity. Record actual approvals, check
identities, adequacy, and results after the events in dated append-only
receipts linked to the plan and contract. A plan or template entry does not
approve a future action or establish that it occurred. Correct receipts with
dated, linked successors; do not edit prior records.

Use the applicable path above: standard/high retains G3, G4 and independent
adequacy; eligible trivial/low uses scope/acceptance authorization and owner/PM adequacy.
Both require the applicable pre-edit result and unchanged GREEN after executable product work.
All
contract cases must
pass with evidence. If a check fails, correct the artifact against the unchanged
contract and rerun the complete contract. Reopen the contract only when the
requirement or contract is wrong. A semantic test or validation change requires
a revised, re-reviewed contract; a purely mechanical correction requires
tester/PE review and new evidence.

A contract change invalidates the affected transitive downstream test,
validation, and implementation or product-artifact subgraph. Unrelated work
remains valid. Preserve superseded IDs and evidence, assign new revision or
lineage IDs to rebuilt artifacts, and record the discarded and rebuilt
relationships. The PM may approve a rebuild affecting at most two downstream
work items only under verified explicit delegation covering that routine
decision. Record the delegation source, scope and count. A count grants
no authority to widen scope, change risk, spend, or make reserved decisions.
If delegation is absent, stale, outside scope, or the limit is exceeded, hold
affected work and obtain a HITL decision: `1. Approve`, `2. Revise`, or
`3. Stop/Defer`. Repeat invalidated reviews and gates before resuming;
unrelated work remains valid.

## Strict Gates

Use the sole [risk-and-control matrix](lifecycle-gates.md#2-classify-risk-before-selecting-gates)
for classification, controls, and eligibility. Use its first-run, N/A, and
missing-reference recovery rule rather than treating missing approval,
reviewer or evidence as an exception.

Interview questions must link to the stated problem. Freeze problem,
measurable outcome, scope, exclusions, risk basis, and acceptance expectations
as separate pre-solution fields. Require complete candidate-delta,
finding, and blocker-ledger identities and links; any missing, empty, duplicate,
dangling/unsafe, relabeled, or no-progress record stops with a minimized reason
and defined recovery.

At every required human approval gate, stop and wait. Present the decision as: `1. Approve`, `2. Revise`, or `3. Stop/Defer`, then record the choice and its evidence. Record a genuinely inapplicable gate in status or the eligible lightweight ledger as specified in the lifecycle reference.

The blocking points below apply where the risk path requires them. Use the
development approver for routine delegated development decisions; owner-reserved
decisions remain with HITL:

| Gate | Required decision before proceeding |
| --- | --- |
| G1 | Scope approval before the approved work is treated as the project boundary. |
| G2 | Where applicable under the matrix, build-package approval before pre-code work is treated as code-ready. |
| G3 | Pre-code review approval before execution can be requested. |
| G4 | Standard/high: explicit development-approver authorization before actual checks or product work. Eligible trivial/low: not applicable; scope authorization instead. |
| G5 | Manual acceptance of finished source before commit or release decisions. |
| G6 | Explicit commit authorization where version control is used. |
| G7 | Explicit owner/HITL deployment authorization before any triggering action for deployment, public release or active install, in addition to authority for the triggering action. |
| G8 | Explicit post-deployment acceptance after independent installed/released verification and runtime-to-approved-source comparison. |
| G9 | Explicit authorization per scoped push, PR, merge or closeout activity; see lifecycle activity mapping and separate CI/effect authority. |

For candidate, CI, merge, promotion, and closeout, follow
[Map gates to activities](lifecycle-gates.md#map-gates-to-activities).
Identify effects before acting and bind decisions to actual scope and exact
identities. A CI workflow automatic on push/PR still needs its separately
verified authority, as do any credential/secret access and egress. Required
PR-only evidence blocked by G5/G6 prerequisites is `not run / hold`,
not N/A or pass.

No agent may provisionally cross a hard gate. Material approved changes reopen the affected risk assessment, reviews, and gates; they do not inherit approval from the earlier version.

## Convergence and Safe Metadata Controls

G1 is the immutable problem and scope baseline. Require a bidirectional
G1-to-G2 trace. One initial G2 may authorize one changed, identity-bound,
in-scope correction; require meaningful measurable progress and stop unchanged,
cosmetic, no-progress, or relabeled-blocker attempts. Every finding must be
plain-language, requirement-traced, and paired with a holistic project-level
solution. Maintain a bounded blocker ledger with stable identity, recurrence,
disposition, progress, and stop state.

Preserve the applicable project review limit. Where it requires one initial
review and one correction/verification pass (such as CONV1-06), obtain an
explicit owner/HITL decision before a third review cycle. A run budget or PM
delegation does not waive that decision.

Conduct one PE/SecOps reconciliation. For ordinary findings, the PM may select
the best-supported remedy or escalate; unresolved security/privacy findings
always go to HITL. Formal G3 requires matching independent PE and SecOps
acceptance of one candidate identity. G3 Revise sends scope/risk to G1 and
solution/evidence to G2; G3 never grants G4.

For standard/high work, the default order is `G3 -> G4 -> actual checks ->
independent PE-CHECK -> required pre-edit result -> product work -> unchanged GREEN`. The Safe Combined Check/RED
Handoff in SKILL.md is the bounded fixture-only alternative; it retains independent
actual-check adequacy and explicit source authorization before product. Actual checks before G4
are prohibited on that path. Eligible trivial/low follows scope authorization and owner/PM
adequacy above. Neither path permits product work before its required adequacy.
Metadata is valid only for an existing repository-relative, non-symlink path
contained by the repository. Reject absolute paths, URLs, `..`, control
characters, missing paths, and containment escapes. Keep evidence minimized and
link history rather than copying transcripts.
