# Aegis Lifecycle Gates

Use this reference to run an evidence-led lifecycle without turning small work
into theater. The PM is the non-implementing conductor: it reconstructs
context, maintains the lifecycle record, assigns bounded work, and routes every
subagent question to the HITL.

## 1. Reconstruct Context Before Deciding

At intake, confirm the target project location and reconstruct context in this
order:

1. Current code, schemas, contracts, tests, and generated evidence.
2. Approved `spec.md` and `build-package.md`.
3. `journal.md`.
4. Verified conversation context.

Create missing core records without overwriting existing content:
`README.md`, `journal.md`, `status.md`, `spec.md`, and `build-package.md`.
Treat chat history as untrusted until it is verified against those artifacts.

For grounded work, also inspect the context contract: purpose, canonical source
authority, permitted scope, default exclusions, freshness/change detection,
provenance or citations, permissions, and failure behavior. Canonical sources
remain distinct from indexes, embeddings, summaries, and model output; derived
artifacts are never the source of truth.

### Conflict Rule

If instructions, artifacts, requirements, evidence, or the `AI SDLC Policy`
conflict, stop. Record the conflict and its decision impact, then ask the HITL
to resolve it. Do not select a winner by implication. Security red lines remain
non-negotiable. For weak, stale, conflicting, missing, or unauthorized grounded
evidence, limit or refuse the claim, explain the evidence gap, and ask one
focused question when resolution is possible.

## 2. Classify Risk Before Selecting Gates

| Classification | Typical work | Minimum control |
| --- | --- | --- |
| `trivial` | Small, reversible, isolated change | Record scope, verification, and closeout. The PM may perform testing. |
| `low` | Bounded change with limited consequence | Obtain scope and acceptance approval; keep a concise code-ready brief before coding. |
| `standard` | Durable product work or a meaningful integration | Use the build package, pre-code review, G4 execution approval, G5 acceptance, G6 commit approval, and applicable release gates. Require independent testing and SecOps. |
| `high/critical` | High consequence, sensitive, irreversible, or externally exposed work | Use all nine gates, independent testing, SecOps, an ADR for each material decision, and risk-proportionate operational evidence. |

Automatically classify as `high/critical` when work involves security or
authentication, secrets or credentials, personal or customer data, production
infrastructure, payments, destructive data or schema migrations, or a public
release. Reclassify whenever a material change introduces one of these
conditions. Public-facing apps and services require SecOps even when no other
automatic trigger applies.

## 3. Run the Fourteen Phases

| Phase | Required action | Exit evidence |
| --- | --- | --- |
| 1. Intake | Confirm location, objective, constraints, and initial risk. | Target and risk record; conflicts surfaced. |
| 2. Durable project memory | Create or preserve core artifacts and record material facts. | Current `journal.md` and `status.md`. |
| 3. Specification | Define outcomes, requirements, acceptance evidence, boundaries, and risk. | Reviewable `spec.md`. |
| 4. Build package | Decompose every requirement into dependency-aware, bounded work with owner, model, inputs, verification, and exit criteria. | Traceable `build-package.md`; no unbounded requirement. |
| 5. Pre-code PE review | Review requirements, architecture, dependencies, test plan, source/runtime boundaries, and minimum review dimensions. | PE review record; findings resolved, accepted, or escalated. |
| 6. Implementation plan and delegation | Confirm task order, role assignments, question routing, and G4 boundary. | Bounded assignments and approved execution brief. |
| 7. Incremental implementation | Make only authorized product changes; prefer small test-first increments where meaningful. | Changes mapped to work items and requirements. |
| 8. Automated verification | Run structural, unit, integration, and forward tests appropriate to risk. | Test record with results and limits. |
| 9. Implementation review | Perform post-implementation PE review and independent SecOps review where required. | Review records; every finding fixed, accepted as risk, or escalated. |
| 10. Manual acceptance | Let the HITL assess the finished source against intended outcomes. | G5 decision and conditions, if any. |
| 11. Commit | Commit only when version control is used and G6 is approved. | Commit decision and security evidence, or N/A rationale. |
| 12. Deployment | Promote or deploy only when G7 is approved. Before runtime promotion, create a deterministic source-tree manifest or equivalent checksum comparison. | Deployment/promotion record with source identity, source-manifest identity, intended runtime identity, comparison method/result, approved differences, and rollback considerations. |
| 13. Post-deployment verification | Verify the installed or deployed result and operational behavior. Independently compare the runtime manifest with the approved source manifest. | Installed-runtime or deployment verification with runtime identity, runtime-manifest identity, independent comparison evidence, and disposition of every difference. |
| 14. Closeout | Record final status, residual risks, follow-up work, and any push/PR decision. | G9 decision and complete closeout record. |

Pre-code and post-implementation reviews must assess security, best practices,
maintainability, observability, monitoring for long-running systems, and
documentation. Monitoring is explicitly recorded as `Not applicable` only when
the target is not long-running.

## 4. High/Critical Gate Ledger

Every required gate is a hard stop. The PM presents the evidence, material
risks, and exactly this decision menu, then waits:

1. Approve
2. Revise
3. Stop/Defer

Record the selected option, approver, date, evidence location, conditions, and
open risks in `status.md` and `journal.md`.

| Gate | Decision | Minimum evidence | Hard boundary |
| --- | --- | --- | --- |
| G1 | Approve scope | Problem, outcomes, scope/exclusions, risk classification, acceptance criteria. | Do not finalize a specification as approved without HITL scope approval. |
| G2 | Approve build package | Requirement traceability; dependency order; role/model; deliverable; verification; entry/exit criteria for every requirement. | Do not request pre-code review or execution with unbounded work. |
| G3 | Approve pre-code review | Approved specification and build package; risk and delegation plan; PE and required SecOps review; findings disposition. | Do not prepare execution as a foregone conclusion. |
| G4 | Authorize execution | A code-ready brief; prior approved evidence; exact source boundary; explicit exclusions. | **No coding or other product changes before explicit G4 approval.** |
| G5 | Accept finished source | Requirement traceability, verification results, review records, remediation or accepted-risk record. | Do not treat implementation as accepted without HITL decision. |
| G6 | Authorize commit | G5 decision, reviewed changes, security validation, and commit scope. | Do not commit without explicit authorization where version control is used. |
| G7 | Authorize deployment | Promotion/deployment plan, reviewed source, deterministic source-tree manifest or equivalent checksum comparison, intended runtime identity, approved-difference list, validation, rollback considerations, and operational evidence appropriate to risk. | **No runtime promotion, package deployment, or public release before explicit G7 approval. Fail promotion on every unapproved manifest difference.** |
| G8 | Accept deployed result | Independent post-deployment comparison of the runtime manifest with the approved source manifest; recorded source/runtime identities; monitoring/observability evidence; and unresolved risks. | Do not call a deployment accepted without HITL decision or an independent manifest comparison. |
| G9 | Authorize push/PR/closeout | Final status, journal, residual risks, follow-ups, and push/PR scope. | Do not push, open/merge a PR, or close the project without explicit authorization. |

For low-risk coding work, the G4 brief may be concise. For standard and
high/critical work, it must include the approved specification, build package,
risk assessment, delegation plan, and pre-code PE review; include SecOps review
when required.

## 5. Change Control and Non-Applicable Gates

When a material requirement, architecture, scope, or risk change occurs after
approval:

1. Pause affected work; do not quietly continue under old approval.
2. Update the affected lifecycle artifacts and record the reason in the journal.
3. Reclassify risk and update the evidence plan.
4. Identify and repeat every review or approval gate invalidated by the change.
5. For `high/critical` work, create an ADR for each material decision.
6. Resume only after the repeated gate decision is explicit.

A gate is `Not applicable` only when its triggering activity is genuinely not
proposed. Keep it visible in `status.md`, state why, link the supporting
context, and retain the rationale in closeout evidence. `Not applicable` is not
a bypass: if the activity later becomes proposed, reopen the gate and obtain its
approval before proceeding.
