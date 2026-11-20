# Aegis Lifecycle Gates

Use this reference to run an evidence-led lifecycle without turning small work
into theater. The PM is the non-implementing conductor: it reconstructs
context, maintains the lifecycle record, assigns bounded work, and routes every
subagent question through the PM to the HITL when needed.
Use the Development Authority definition in SKILL.md for the development approver:
owner by default, explicitly delegated PM only within recorded scope; reserved
owner decisions and production promotion do not transfer.

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

### Master-Specification Rule

Every governed project has exactly one current repository-root `spec.md`. It is
the sole current requirements and architecture authority. Create it once at
project setup when absent; never create a second, enhancement-specific, or
replacement specification.

Before material discovery or planning, read and validate that existing file. A
material request changes product law only through an approved amendment to the
same file. A new per-run build package is required for every governed run,
including a concise package for trivial work, but it is immutable execution
evidence, never a competing specification.
It must name the spec path, revision/date, pre-execution identity, covered
requirement IDs, fixed creation or decision context, and
predecessor/successor when applicable. A package does not own mutable current
gate state; record that state in `status.md` and append-only gate receipts.

At G2, record the spec and package identities in an append-only receipt. Verify
them before applicable G3 and again immediately before authorized edits. After
execution authorization, final-spec acceptance requires its approval receipt, an explicit map from every final spec
change to approved requirement IDs or an approved amendment, and a final digest
recorded at G5. The final digest is evidence of the resulting approved spec; it
need not equal the pre-execution identity. A pre-execution identity mismatch, unsafe
metadata, missing/unknown/duplicate/retired requirement ID, competing sidecar,
unmapped final change, or altered historical inventory is a hard stop.

Keep an append-only authority registry and checksum inventory for project
scopes, packages, briefs, reviews, verification, ADRs, receipts, manifests, and
migration records. Classify each record as `current`, `decision`, `execution`,
or `historical`. Every inventory declares an evidence cutoff: a changed, missing,
or unclassified record at or before that cutoff is a hard stop; records created
after it are pending for the next dated successor inventory. Preserve
superseded evidence; correct a record with a dated successor rather than
rewriting approved history.

## 2. Classify Risk Before Selecting Gates

The trivial/low shortcut is eligible only for non-public-facing work without
security/privacy-sensitive triggers, as defined in SKILL.md. Public-facing work
uses at least standard G4 and independent review/testing controls; sensitive
work follows its applicable standard/high controls even if otherwise low consequence.

Convergence records are complete only when interview questions link to the
stated problem and protected G1 fields are frozen separately from solution.
Brief summaries are non-normative and non-exhaustive; the exact canonical C03,
C05, and C07 schemas below govern. Missing, empty, duplicate, dangling/unsafe,
relabeled, or no-progress records fail closed and stop the branch with defined
recovery.

The exact schemas are:

- **C01 immutable G1/question:** `g1_id`, `g1_digest`, `problem`,
  `measurable_outcome`, `scope`, `exclusions`, `risk_basis`,
  `acceptance_expectations`; each question has `question_id`,
  `question_text`, `problem_basis_id`, `derivation_reason`.
- **C03 candidate delta:** `candidate_id`, `candidate_digest`, `predecessor_id`,
  `predecessor_digest`, `delta_id`, `artifact_path`, `before_summary`,
  `after_summary`, `change_kind`, `driving_finding_id`, `affected_g1_ids`,
  `affected_conv_ids`, `affected_ac_ids`, `affected_check_ids`,
  `evidence_pointers`, `scope_classification`, `lineage_reason`.
- **C05 finding:** `finding_id`, `human_readable_finding`, `evidence_pointers`,
  `affected_g1_ids`, `affected_conv_ids`, `affected_ac_ids`,
  `affected_check_ids`, `severity`, `reviewer_set`, `owner`,
  `direct_work_impact`, `dependent_work_impact`, `gate_impact`,
  `security_privacy_impact`, `verification_impact`, `documentation_impact`,
  `operations_monitoring_applicability`, `downstream_effects`,
  `recovery_rollback`, `holistic_remedy`, `disposition`,
  `stop_escalation_reason`.
- **C07 blocker ledger:** `blocker_id`, `source_finding_ids`,
  `underlying_identity`, `recurrence_count`, `affected_requirement_ids`,
  `affected_check_ids`, `severity`, `reviewer_set`, `owner`,
  `holistic_remedy`, `disposition`, `evidence_pointers`, `progress_state`,
  `next_action`, `direct_work_impact`, `dependent_work_impact`, `gate_impact`,
  `stop_escalation_reason`.

Every field is present exactly once, nonempty, and resolves safely. Missing,
empty, or duplicate fields fail as `C01-MISSING:<field>`/
`C01-EMPTY:<field>`, `C03-MISSING:<field>`/`C03-EMPTY:<field>`/
`C03-DUPLICATE:<field>`, `C05-MISSING:<field>`/`C05-EMPTY:<field>`/
`C05-DUPLICATE:<field>`, or `C07-MISSING:<field>`/`C07-EMPTY:<field>`/
`C07-DUPLICATE:<field>` and stop. Also stop on `C01-UNDERIVED-QUESTION`,
`C01-REASON-MISMATCH`, `G1-PRESSURE:<field>`, `C03-UNMAPPED-DELTA`,
`C03-UNCHANGED-CANDIDATE`, `C03-UNSAFE-PATH`, `C05-LOCAL-ONLY-REMEDY`,
`C05-DANGLING-ID`, `C05-UNSAFE-EVIDENCE-POINTER`,
`C07-RELABELLED-BLOCKER`, `C07-NO-PROGRESS-PATH`, and
`C07-DANGLING-FINDING`.

| Classification | Typical work | Minimum control |
| --- | --- | --- |
| `trivial` | Small, reversible, isolated change | Record scope, verification, and closeout. The PM may perform testing. |
| `low` | Bounded change with limited consequence | Obtain scope and acceptance approval; keep a concise code-ready brief before coding. |
| `standard` | Durable product work or a meaningful integration | Use the build package, pre-code review, G4 execution approval, G5 acceptance, G6 commit approval, and applicable release gates. Require independent testing and SecOps. |
| `high/critical` | High consequence, sensitive, irreversible, or externally exposed work | Use all nine gates, independent testing, SecOps, an ADR for each material decision, and risk-proportionate operational evidence. |

Classify work before choosing ceremony: `trivial`, `low`, `standard`, or
`high/critical`. Escalate to `high/critical` for materially sensitive-data handling or exposure,
security/authentication, secrets or credentials, production infrastructure,
payments, destructive data/schema migrations, or public release. Assess actual sensitivity, handling changes, exposure and consequence.
The mere presence of ordinary authorized internal, public or synthetic data alone
is not a leak or automatic high/critical classification. Internal use is never an
exemption for genuine security or sensitive-data risks. Public availability does
not grant permission for new sharing; platform transmission/confirmation rules remain.

Eligible trivial/low work uses explicit scope/acceptance authorization, concise brief and
validation plan, owner/PM adequacy and validation; G4 is not applicable with
recorded rationale. Standard/high work retains applicable G3/G4 and independent
review/testing. Apply phases and ledgers only as required by that risk path.

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
| 10. Manual acceptance | Let the development approver assess the finished source against intended outcomes. | G5 decision and conditions, if any. |
| 11. Commit | Commit only when version control is used and G6 is approved. | Commit decision and security evidence, or N/A rationale. |
| 12. Deployment | Promote or deploy only when G7 is approved. Before runtime promotion, create a deterministic source-tree manifest or equivalent checksum comparison. | Deployment/promotion record with source identity, source-manifest identity, intended runtime identity, comparison method/result, approved differences, and rollback considerations. |
| 13. Post-deployment verification | Verify the installed or deployed result and operational behavior. Independently compare the runtime manifest with the approved source manifest. | Installed-runtime or deployment verification with runtime identity, runtime-manifest identity, independent comparison evidence, and disposition of every difference. |
| 14. Closeout | Record final status, residual risks, follow-up work, and any push/PR decision. | G9 decision and complete closeout record. |

Pre-code and post-implementation reviews must assess security, best practices,
maintainability, observability, monitoring for long-running systems, and
documentation. Monitoring is explicitly recorded as `Not applicable` only when
the target is not long-running.

### Contract-First Gate Integration

Every product-changing work item identifies a contract in the intake, master
specification traceability, and run-specific build package. Executable work
uses a test contract; non-executable work uses an artifact-appropriate
validation contract.

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

Applicable G2 binds contracts, dependencies and rebuild boundaries; G3 reviews
planned checks, dependencies and artifact order. G5-G9 trace evidence to contracts
and requirements. Material contract change reopens affected gates.

All contract cases, including negative and edge cases, must pass with evidence.
If a check fails, correct the artifact against the unchanged contract and rerun
the complete contract. A semantic test or validation change requires a revised
and re-reviewed contract; a mechanical correction requires tester/PE review and
new evidence.

A contract change invalidates the affected transitive downstream test,
validation, and implementation or product-artifact subgraph, while unrelated
work remains valid. Preserve prior IDs and evidence and assign new revision or
lineage IDs to rebuilt artifacts. The PM may approve rebuilds affecting two or
fewer downstream work items; more than two requires a HITL decision using the
standard numbered menu. Record the invalidation, discarded artifacts, rebuilt
artifacts, and evidence lineage.

### SecOps PII Check

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

## 4. High/Critical Gate Ledger

Every applicable gate requires a recorded authorized decision. For required
human approval, the PM presents evidence, material risks and this menu, then waits:

1. Approve
2. Revise
3. Stop/Defer

Record the selected option, approver, date, evidence location, conditions, and
open risks in `status.md` and `journal.md`.

### Canonical Gate Display

Use the following display form for every newly generated gate prompt, gate
record, and status reference. The name clarifies the decision; the ID remains
the authoritative identifier.

| Base gate | Canonical display |
| --- | --- |
| G1 | Scope Approval (G1) |
| G2 | Build-Package Approval (G2) |
| G3 | Pre-Code Review (G3) |
| G4 | Execution Authorization (G4) |
| G5 | Manual Acceptance (G5) |
| G6 | Commit Authorization (G6) |
| G7 | Deployment Authorization (G7) |
| G8 | Post-Deployment Acceptance (G8) |
| G9 | Push/PR/Closeout Authorization (G9) |

For an approved increment-specific gate, retain the full identifier and use the
recognized base-gate purpose, for example `Scope Amendment (G1-ENH-002)`. Do
not infer a gate name or authority from arbitrary user-supplied text. Do not
renumber gates or rewrite historical evidence solely to normalize display text.

| Gate | Decision | Minimum evidence | Hard boundary |
| --- | --- | --- | --- |
| Scope Approval (G1) | Approve scope | Problem, outcomes, scope/exclusions, risk classification, acceptance criteria. | Do not finalize a specification as approved without development-approver scope approval. |
| Build-Package Approval (G2) | Approve build package | Requirement traceability; dependency order; role/model; deliverable; verification; entry/exit criteria for every requirement. | Do not request pre-code review or execution with unbounded work. |
| Pre-Code Review (G3) | Approve pre-code review | Approved specification and build package; risk and delegation plan; PE and required SecOps review; findings disposition. | Do not prepare execution as a foregone conclusion. |
| Execution Authorization (G4) | Authorize execution | A code-ready brief; prior approved evidence; exact source boundary; explicit exclusions. | **Standard/high: no actual checks or product before development-approver G4. Eligible trivial/low: G4 not applicable; explicit scope authorization instead.** |
| Manual Acceptance (G5) | Accept finished source | Requirement traceability, verification results, review records, remediation or accepted-risk record. | Do not treat implementation as accepted without development-approver decision. |
| Commit Authorization (G6) | Authorize commit | G5 decision, reviewed changes, security validation, and commit scope. | Do not commit without explicit authorization where version control is used. |
| Deployment Authorization (G7) | Authorize deployment | Promotion/deployment plan, reviewed source, deterministic source-tree manifest or equivalent checksum comparison, intended runtime identity, approved-difference list, validation, rollback considerations, and operational evidence appropriate to risk. | **No runtime promotion, package deployment, or public release before explicit owner/HITL G7 approval. Fail promotion on every unapproved manifest difference.** |
| Post-Deployment Acceptance (G8) | Accept deployed result | Independent post-deployment comparison of the runtime manifest with the approved source manifest; recorded source/runtime identities; monitoring/observability evidence; and unresolved risks. | Do not call a deployment accepted without owner/HITL decision or an independent manifest comparison. |
| Push/PR/Closeout Authorization (G9) | Authorize push/PR/closeout | Final status, journal, residual risks, follow-ups, and push/PR scope. | Do not push, open/merge a PR, or close the project without explicit authorization. |

For eligible trivial/low work, the scope/acceptance brief may be concise; G4 is not
applicable. For standard and
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

A gate is `Not applicable` when the risk path excludes it or its triggering
activity is genuinely not proposed. Keep it visible in `status.md`, state why, link the supporting
context, and retain the rationale in closeout evidence. `Not applicable` is not
a bypass: reopen when a changed risk path makes the gate applicable, or when a
previously absent activity is proposed and the gate applies to that activity.
Obtain approval before proceeding past the newly applicable gate; unchanged
eligible low-risk coding does not itself make G4 applicable.

## G2/G3 Candidate Convergence

Treat approved G1 problem, outcomes, scope, and risk as immutable. Build a
bidirectional trace from each G1 assertion to G2 requirements/acceptance checks
and back; missing, extra, renamed, or invented links stop the run. One initial
G2 authorizes an in-scope correction only with a new candidate identity,
immutable lineage, meaningful measurable progress, and complete
finding/blocker disposition. Unchanged, cosmetic, no-progress, or relabeled
blocker candidates cannot be re-reviewed; there is no numeric iteration cap.

Every finding is plain-language, requirement-traced, and paired with a
holistic project-level solution. Keep a bounded blocker ledger recording stable
identity, recurrence, disposition, progress evidence, and stop state. PE and
SecOps must independently accept the same identity before formal G3. Reconcile
once; the PM may choose an ordinary best-supported remedy or escalate, but
unresolved security/privacy always requires HITL. G3 Revise routes scope/risk
to G1 and solution/evidence to G2; G3 never grants G4.

For standard/high, the default dependency trace is `G3 -> G4 -> actual checks ->
independent PE-CHECK -> required pre-edit result -> product work -> unchanged GREEN`. The Safe Combined Check/RED
Handoff in SKILL.md permits the approved fixture-only variant, with independent
actual-check adequacy and explicit source authorization still before product. Reject actual checks before
applicable G4, product before adequacy, and G3-as-G4 wording. Eligible trivial/low follows
the scope-authorized owner/PM path above, including the required pre-edit result for its work type. Metadata must be an existing,
repository-relative, non-symlink path contained within the repository; reject
absolute paths, URLs, `..`, control characters, missing paths, and containment
escapes. Link prior records instead of dumping history.
