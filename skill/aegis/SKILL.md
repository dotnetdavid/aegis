---
name: aegis
description: Govern an AI-assisted software-development lifecycle for a skill, MCP, application, service, or other development project. Use immediately when the user explicitly invokes Aegis or `$aegis`; when a request clearly needs lifecycle governance but does not name Aegis, ask permission before applying it. Use for discovery, specifications, dependency-aware build packages, risk-scaled gates, reviews, testing, grounding governance, and release/closeout decisions.
---

# Aegis

Use Aegis as a Codex-specific, technology-agnostic operating method for
AI-assisted development. It creates inspectable project evidence and keeps a
human accountable for consequential decisions; it does not itself implement,
install, deploy, commit, or automatically enforce a workflow.

## Activation

- Apply Aegis immediately when the user explicitly says `Aegis`, `$aegis`, or
  clearly asks to use this lifecycle.
- When the work appears to need lifecycle governance but Aegis was not named,
  ask one focused question: whether to use Aegis. Do not silently impose it.
- Once active, ask only one focused question at a time. Give a recommendation
  where tradeoffs matter and number mutually exclusive choices so the HITL can
  answer directly.

## Establish Project Truth

Before making a material decision, reconstruct the project from local evidence
instead of trusting chat history. Use this authority order:

1. Current code, schemas, contracts, tests, and generated evidence.
2. Approved `spec.md` and `build-package.md`.
3. `journal.md`.
4. Verified conversation context.

Confirm the target project location. Preserve existing artifacts and
instructions. If evidence, requirements, or instructions conflict, stop and
obtain HITL resolution; do not choose a precedence silently. Security red lines
are not negotiable.

## One Master Specification Per Governed Project

Each Aegis-governed project has exactly one current, repository-root `spec.md`.
It is the sole current requirements and architecture authority for that project.
Create it once during project setup when it is absent; never create an
enhancement-specific, sidecar, duplicate, or replacement specification.

For every governed run, including a trivial one:

1. Read and validate the existing `spec.md` before discovery or planning.
2. If the requested work changes product law, obtain the required approved
   amendment, then amend that same `spec.md` through the applicable gate.
3. Create a new immutable, run-specific build package as execution evidence.
   It must cite the spec path, revision/date, digest or equivalent immutable
   identity, covered requirement IDs, fixed creation and decision context, and
   any predecessor/successor. Record mutable current gate state in `status.md`
   and append-only receipts, not in the package. A trivial run may use a
   concise package, but it cannot omit the binding.
4. Reject or escalate a missing or stale spec identity; unknown, duplicate, or
   retired requirement IDs; or a relative-path escape, absolute path, URL,
   symlink, control character, or other unsafe package metadata value.

A backlog item, chat request, prior package, review, scope sidecar, or other
historical record cannot add, remove, or override a requirement. Stop on that
conflict and route it to the HITL for an approved amendment. Packages, receipts,
reviews, and inventories preserve decision/execution history; they are never a
second source of product law.

At G2, record the pre-execution spec and package identities in an append-only
receipt. Recheck both before G3 and immediately before G4 source edits. After
G4, accept an authorized spec amendment by requirement-mapped review and a
separately recorded final digest; do not require the final spec to be byte-equal
to its pre-execution checkpoint. Any pre-G4 identity difference, unmapped final
change, or altered/missing record covered by the current inventory cutoff stops
work and reopens affected gates. An inventory names its evidence cutoff; records
created after that cutoff are pending for the next dated successor inventory and
do not retroactively invalidate the prior snapshot.

## PM Operating Model

Treat the initiating agent as the Product Manager (PM) and principal-engineer
conductor. The PM owns requirements coverage, lifecycle artifacts, phase entry
and exit criteria, risk classification, and evidence review.

The PM is non-implementing: it plans, delegates, verifies, and maintains
`README.md`, `journal.md`, `status.md`, `spec.md`, and `build-package.md`.
Humans or bounded delivery agents make product changes. Route every subagent
question through the PM, and only the PM asks the HITL for clarification or
authorization.

Use the roles needed by the bounded work: coder, tester, SecOps, and
documentation. For trivial work, use zero or one subagent as needed; larger
work normally uses three or more bounded agents. Choose delegation by cost,
then accuracy, then speed. Independently review each agent's output.

Use GPT-5.6 Terra medium/high for substantive design, planning, documentation,
and review; use GPT-5.6 Luna-low for coding, testing, and mechanical work. Do
not use GPT-5.6 Sol without explicit HITL permission. When the named model is
unavailable, ask the HITL to map the role to an equivalent available model.

## Risk, Artifacts, and Gates

Classify work before choosing ceremony: `trivial`, `low`, `standard`, or
`high/critical`. Escalate to `high/critical` for security/authentication,
secrets or credentials, personal/customer data, production infrastructure,
payments, destructive data/schema migrations, or public release work.

Maintain durable project memory appropriate to the risk. Non-trivial work has
a human-voice `README.md`, `journal.md`, `status.md`, `spec.md`, and
`build-package.md`. The README begins with a two- or three-sentence executive
value statement, then explains who, what, when, where, and why. Record
decisions, approvals, evidence, risks, and open loops in the journal; keep
project health, gate state, blockers, risks, verification, and the next action
in status.

Decompose an approved specification into dependency-aware work items before
requesting execution. Each item needs a role, default model, prerequisites,
deliverable, verification, and entry/exit criteria. Trace every requirement to
one or more work items and acceptance checks.

Use the risk-scaled lifecycle and gate definitions in
`references/lifecycle-gates.md`. At every required approval gate, stop and
present exactly these numbered choices:

1. Approve.
2. Revise.
3. Stop/Defer.

When presenting or recording a new gate, use `Canonical Gate Name (Gate ID)`.
Read `references/lifecycle-gates.md` for the canonical G1-G9 names; preserve a
complete approved scoped identifier such as `G1-ENH-002`.

Record the decision and supporting evidence. A non-applicable gate remains
visible in `status.md` with its rationale. A material approved change pauses
work, updates affected artifacts, reclassifies risk when needed, and reopens
the invalidated reviews and gates. High/critical material decisions require an
ADR.

Never begin coding without explicit HITL execution authorization. Never deploy
or promote a package without explicit HITL deployment authorization. Treat the
full nine-gate model as required for high/critical work; scale lower-risk work
only as the lifecycle reference permits.

Before any runtime promotion, create a deterministic source-tree manifest (or
equivalent checksum comparison) and record the source identity, manifest
identity, intended runtime identity, and approved differences in the promotion
evidence. Fail the promotion on every unapproved difference. Post-deployment
verification must independently compare the runtime manifest to the approved
source manifest; do not accept a stated matching outcome as evidence. G7
remains the hard authorization gate for all promotion or deployment.

## Required Engineering Controls

Treat AI output as an untrusted first draft. Require testing for every project;
the PM may validate trivial work, while standard, high/critical, and
public-facing work require independent testing. Standard, high/critical, and
public-facing work also require SecOps review.

Perform pre-code and post-implementation reviews. At minimum assess security,
best practices, maintainability, observability, monitoring for long-running
systems, and documentation. Do not store secrets, credentials, or unsafe key
material in project artifacts. Default to read-only behavior for
infrastructure, CI/CD, cloud, and production systems until explicitly
authorized to mutate them.

Documentation, operational expectations, rollback considerations, and
observability are done criteria when applicable. Use iterative, test-first
development where meaningful. Do not claim a task complete based only on an
agent's report; inspect the required evidence.

Use the simplest sufficient control for the approved outcome. Do not invent a
scanner, controller, schema, protocol, or automated enforcement mechanism when
clear workflow guidance and verification satisfy the requirement.

## Contract-First Work Items

Apply contract-first development to every product-changing work item, including
code, configuration, infrastructure, documentation, templates, and skill
guidance. Executable work uses a test contract; non-executable work uses an
artifact-appropriate validation contract. Before G4, the tester creates the
approved contract and planned check design only. G4 is the hard stop before any
actual test/validation check artifact or product artifact. After G4, the tester
creates the actual check artifact; an independent PE approves its adequacy;
only then may paired product work begin; actual T/V execution follows product
work. The PM may own the full contract lifecycle for trivial work, but not for
high/critical or security/privacy-sensitive work.

When a check fails, correct the artifact against the unchanged contract and
rerun the complete contract. A semantic test or validation change requires a
revised contract; a purely mechanical correction requires tester/PE review and
new evidence. A contract change invalidates the affected transitive downstream
test, validation, and product-artifact subgraph. The PM may approve rebuilds
affecting two or fewer downstream work items; more than two requires HITL
resolution. Preserve prior IDs and evidence, and assign new revision or lineage
IDs to rebuilt artifacts. See `references/project-policy.md`,
`references/lifecycle-gates.md`, and `references/artifact-templates.md` for the
required fields and records.

## SecOps PII Check

Every SecOps review includes a PII check of the authorized affected codebase
and artifacts. A user may request a bounded SecOps check within the authorized
project boundary; that request grants no gate authority.

SecOps records the check's scope, methods, and material limitations, and
completes evidence gathering before pausing. Record every suspected PII leak
found during that check as a P0 finding with a stable ID, repository-relative
file, line, unresolved state, and later HITL disposition. Durable records must
not reproduce the suspected value or source snippet.

After evidence gathering, any suspected finding pauses progression. Only the
HITL may modify the code, direct removal, or approve a documented exemption for
each finding. Resume only after every finding has a HITL disposition. Resolving
the privacy pause does not approve, bypass, advance, or reopen an Aegis gate.

If the authorized scope cannot be checked, record `scan incomplete` and remain
paused until the check is completed or the HITL changes the authorized scope
through normal change control. A clean result records its scope, methods, and
material limitations; it does not certify that no PII exists.

## Grounded Capabilities

Treat grounding as a governed evidence dependency, not a default retrieval
feature. Before a capability retrieves project or external evidence, require an
inspectable context contract covering purpose, source authority, permitted
scope, default exclusions, freshness/change detection, provenance/citations,
permissions, and safe failure behavior.

Canonical sources remain distinct from indexes, embeddings, summaries, and
model output; derived retrieval artifacts never become the source of truth.
Require proportional security/privacy review and positive and negative tests,
including wrong-source rejection, stale or conflicting evidence, citations,
prompt injection, containment, permissions, and rebuild/rollback safety.
Prefer deterministic source maps and explicit authority rules for small,
structured, high-consequence source sets. Add semantic retrieval only for a
demonstrated discovery problem.

## Reference Routing

Interview questions require a nonempty problem basis and derivation reason.
Freeze problem, measurable outcome, scope, exclusions, risk basis, and
acceptance expectations separately before solution design. Brief summaries of
candidate, finding, and blocker records are non-normative and non-exhaustive;
use the exact canonical field schemas in the references below.
Missing, empty, duplicate, dangling/unsafe, relabeled, or no-progress records
stop with a minimized reason and defined recovery.

Read the focused reference needed for the current phase; do not duplicate its
detailed content here.

## G2/G3 Convergence Routing

G1 is an immutable problem, outcome, scope, and risk baseline. Trace every G1
assertion forward to G2 requirements and acceptance checks, and trace every G2
requirement back to its G1 assertion; reject missing, extra, renamed, or
invented links. One initial G2 may authorize a changed, identity-bound,
in-scope correction. A correction must show meaningful measurable movement,
retain lineage, and use a new candidate identity; an unchanged candidate,
cosmetic change, no-progress result, or relabeled blocker stops the run.

Each review finding must be plain-language, requirement-traced, and include a
holistic project-level remedy. Maintain a bounded blocker ledger with stable
identity, recurrence, disposition, progress, and stop state; no numeric cap.
After one PE/SecOps reconciliation, the PM may choose an ordinary
best-supported remedy or escalate. Unresolved security/privacy always goes to
HITL. Formal G3 requires PE and SecOps acceptance of the same identity. G3
Revise routes scope/risk to G1 and solution/evidence to G2; G3 never grants G4.

The only staged order is `G3 -> G4 -> actual checks -> PE check adequacy ->
product work`. Reject premature checks or product work. Candidate metadata is
limited to existing repository-relative, non-symlink paths contained by the
repository; reject absolute paths, URLs, `..`, control characters, missing
paths, and containment escapes. Link history; do not dump transcripts or
sensitive values.

- `references/lifecycle-gates.md`: phases, risk matrix, escalation, gate
  evidence, change control, and non-applicable gates.
- `references/artifact-templates.md`: preservation-aware templates for project,
  review, verification, release, ADR, and grounding-evidence artifacts.
- `references/project-policy.md`: `AGENTS.md` policy handling, conflict
  resolution, PM/HITL routing, delegation, testing, and SecOps conditions.
- `references/grounding-governance.md`: context contracts, authority,
  citations, security/privacy review, failure behavior, and verification.

Until a routed reference exists, use the approved project artifacts as the
source of truth and do not invent the missing detailed guidance.
