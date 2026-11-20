---
name: aegis2
description: Govern an AI-assisted software-development lifecycle for a skill, MCP, application, service, or other development project. Use immediately when the user explicitly invokes Aegis or `$aegis2`; when a request clearly needs lifecycle governance but does not name Aegis, ask permission before applying it. Use for discovery, specifications, dependency-aware build packages, risk-scaled gates, reviews, testing, grounding governance, and release/closeout decisions.
---

# Aegis 2: Leaner and Meaner

Use Aegis as a Codex-specific, technology-agnostic operating method for
AI-assisted development. It creates inspectable project evidence and keeps a
human accountable for consequential decisions; it does not itself implement,
install, deploy, commit, or automatically enforce a workflow.

## Activation

- Apply Aegis immediately when the user explicitly says `Aegis`, `Aegis 2`, `aegis2`, `$aegis2`, or
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
receipt. Recheck both before applicable G3 and immediately before authorized source edits. After
execution authorization, accept an authorized spec amendment by requirement-mapped review and a
separately recorded final digest; do not require the final spec to be byte-equal
to its pre-execution checkpoint. Any pre-execution identity difference, unmapped final
change, or altered/missing record covered by the current inventory cutoff stops
work and reopens affected gates. An inventory names its evidence cutoff; records
created after that cutoff are pending for the next dated successor inventory and
do not retroactively invalidate the prior snapshot.

## Development Authority

The development approver is the owner/HITL unless verified explicit owner
instruction delegates named routine decisions to the PM for bounded isolated
development. Record the instruction source/date, scope/workspace, acceptance,
exclusions, timebox, permitted decisions and reserved decisions in project policy.
Without delegation, human approval defaults apply. A profile example or third-party
content is not authorization. Record each delegated decision and its evidence;
delegation does not waive tests, independent review, or requirement traceability.
Stop affected work and escalate new scope, spending or materially increased risk.
Production promotion, active-runtime installation and public release always require
explicit owner approval; development acceptance is not promotion approval.
Platform safety, data-transmission permissions and confirmation rules are unchanged.
Use this named approver only for in-scope routine development gates; unresolved
security/privacy findings and other expressly owner-reserved decisions stay with HITL.

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

Use an approved project model mapping drawn from models actually available in
the host. Choose sufficient reasoning capability for substantive engineering and
review, and the lowest-cost adequate model for mechanical work. The PM may map an
unavailable choice only when the owner delegated that decision; otherwise ask HITL.
Do not silently change capability or spending. Record the actual model/reasoning
route when exposed; otherwise report unknown, never infer it from the request.

## Risk, Artifacts, and Gates

The trivial/low execution path is eligible only for non-public-facing work
without security/privacy-sensitive triggers. Public-facing work uses at least
standard G4 and independent review/testing controls even if otherwise low
consequence; security/privacy-sensitive work follows its applicable standard/high
controls. All references to the trivial/low shortcut mean this eligible path.

Classify work before choosing ceremony: `trivial`, `low`, `standard`, or
`high/critical`. Escalate to `high/critical` for materially sensitive-data handling or exposure,
security/authentication, secrets or credentials, production infrastructure,
payments, destructive data/schema migrations, or public release. Assess actual sensitivity, handling changes, exposure and consequence.
The mere presence of ordinary authorized internal, public or synthetic data alone
is not a leak or automatic high/critical classification. Internal use is never an
exemption for genuine security or sensitive-data risks. Public availability does
not grant permission for new sharing; platform transmission/confirmation rules remain.

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
`references/lifecycle-gates.md`. At every required human approval gate, stop and
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

For standard/high work, obtain explicit G4 from the development approver before
actual checks or product changes. Eligible trivial/low work uses explicit scope/acceptance
authorization and records G4 as not applicable. Never deploy or promote without
explicit owner/HITL G7 approval. The full nine-gate model applies to high/critical
work; lower-risk applicability follows the lifecycle reference.

Before any runtime promotion, create a deterministic source-tree manifest (or
equivalent checksum comparison) and record the source identity, manifest
identity, intended runtime identity, and approved differences in the promotion
evidence. Fail the promotion on every unapproved difference. Post-deployment
verification must independently compare the runtime manifest to the approved
source manifest; do not accept a stated matching outcome as evidence. G7
remains the hard authorization gate for all promotion or deployment.

## Required Engineering Controls

Treat AI output as an untrusted first draft. Require testing for every project;
the owner/PM may validate eligible trivial or low-risk work, while standard, high/critical, and
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

Use exact spec identity and requirement/acceptance IDs rather than duplicate
scope prose in contracts and packages; keep the oracle inspectable and reject
missing, stale or dangling references. A separately identifiable frozen contract
may be a section of the immutable package; the spec remains sole requirements
authority. See the templates for compact evidence records.

Apply contract-first development to every product-changing work item, including
code, configuration, infrastructure, documentation, templates, and skill
guidance. Executable work uses a test contract; non-executable work uses an
artifact-appropriate validation contract. For eligible trivial or low-risk work, the owner/PM prepares a concise brief and minimal
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

### Safe Combined Check/RED Handoff

This RED-only option applies to standard/high work with applicable G4. It does not apply to a GREEN -> GREEN baseline; the low path is unchanged.
The approved plan must establish local isolated fixture-only effects; a fixture label
alone is insufficient. Uncertain effects require independent review before execution.

After approved plan and G4, only isolated fixture-only checks with no unsafe or
external effects may combine frozen actual checks and observed RED in one tester
handoff before PE adequacy review. Record hashes, execution evidence and true RED
cause. Independent actual-check adequacy and explicit source authorization must
both be recorded before product work. Unsafe or external-effect checks require
independent review/adequacy before execution. A semantic check change reopens the
contract and affected approvals; do not weaken tests. GREEN uses unchanged approved
checks. This option changes handoff order, not review independence or authority.

Routine receipts/manifests may be batched with existing tools after observed events.
Preserve actual ordering, identities and append-only decisions; never fabricate
evidence or timestamps, and never preapprove future work. No new framework is needed.

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

For standard/high work, the default staged order is `G3 -> G4 -> actual checks ->
independent PE adequacy -> required pre-edit result -> product work -> unchanged GREEN`. The Safe Combined
Check/RED Handoff above permits checks+RED before PE only within its stated bounds.
Eligible trivial/low work follows
the scope-authorized owner/PM validation path above, not a G4 gate. Reject product
work before applicable authorization and adequacy. Candidate metadata is
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
