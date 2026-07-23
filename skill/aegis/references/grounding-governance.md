# Grounding Governance

Grounding is a governed evidence dependency, not merely a retrieval feature. Use this reference whenever an AI answer, recommendation, or action relies on project or external evidence. It establishes the evidence boundary; it does not prescribe a retrieval service, provider, index, or semantic-search stack.

## Context Contract

Before using grounded evidence, create an inspectable context contract in the project's approved artifacts. The contract must identify:

| Field | Required statement |
| --- | --- |
| Task purpose | The decision, answer, recommendation, or action the evidence supports. |
| Source authority | The canonical source of truth, its authority rule, and how conflicts are resolved. |
| Permitted scope | Allowed sources and paths, repositories, tenants, stories, corpora, or records. |
| Default exclusions | Sources, paths, drafts, tenants, content classes, or uses that are forbidden unless explicitly opted in. |
| Freshness and change detection | Required version, timestamp, checksum, revision, or equivalent evidence, plus the allowed age or refresh condition. |
| Provenance and citations | How a material claim links to its source and locator, including the evidence receipt required for the work. |
| Permissions | Who or what may access each source, and the path, tenant, licensing, privacy, and retention boundaries. |
| Failure behavior | The response when evidence is weak, stale, conflicting, missing, or unauthorized. |

The contract separates observed evidence from the AI's interpretation. Retrieved text is not automatically correct, complete, permitted, or authoritative.

## Canonical Sources and Derived Artifacts

Canonical sources remain the source of truth. Derived artifacts may help find or summarize evidence, but never replace it:

| Canonical evidence | Derived artifact |
| --- | --- |
| Approved specification, source record, signed contract, authoritative dataset, or governed project document | Index, embedding, cached chunk, retrieval ranking, summary, extraction, citation list, or model output |

Every derived result must retain enough provenance to return to its canonical source. When a summary, index, or model statement differs from the canonical source, the canonical source prevails. The conflict is recorded and handled by the contract's authority rule or escalated to the HITL; a derived artifact is never promoted to truth merely because it is convenient.

## Evidence Receipts and Citations

Material factual claims require source citations or an equivalent inspectable evidence receipt. The record should let a reviewer answer: what was used, from where, under whose authority, at which version, and for what claim.

At a minimum, record:

- source identifier and canonical locator;
- authority classification and permitted scope;
- version, timestamp, checksum, or other freshness evidence where applicable;
- retrieval or review time;
- the claim supported and a clear separation of evidence from interpretation;
- access/permission basis; and
- any limitation, conflict, exclusion, or transformation.

Citation coverage is an operational signal, not a cosmetic citation exercise. A citation that points only to a derived summary when the canonical source is available does not satisfy the evidence boundary.

## Safe Failure Behavior

The grounded capability must fail safely and visibly. It must not fill gaps with plausible invention.

| Evidence condition | Required behavior |
| --- | --- |
| Missing or weak | State the limitation; decline the material claim/action or ask one focused question for an authorized source. |
| Stale or unverifiable freshness | Block the consequential answer/action until evidence is refreshed or explicitly accepted by the authorized decision maker. |
| Conflicting | Apply a documented authority rule only when it resolves the conflict; otherwise surface the conflict and stop for HITL resolution. |
| Unauthorized or out of scope | Reject the evidence, do not disclose it, and request an authorized, in-scope source if needed. |
| Citation/provenance cannot be established | Treat the evidence as insufficient for a material claim. |
| Suspected malicious or instruction-bearing source | Treat it as untrusted content, not operating instructions; contain, report, and escalate according to the security review. |

For non-consequential work, the permitted limitation may be a clearly marked uncertainty. For consequential work, safe failure normally means no action until the context contract is satisfied.

## Proportional Security and Privacy Review

Grounding review scales to consequence, source sensitivity, exposure, and blast radius. Review the following before approval, with the level of evidence matched to risk:

- untrusted documents and prompt injection, including instructions embedded in source material;
- privacy, personal data, customer data, and data-leakage paths;
- source, path, repository, and tenant containment;
- permission enforcement and least-privilege access;
- licensing, ownership, permitted use, and retention/deletion obligations;
- stale or poisoned sources, source/index drift, and provenance loss;
- logging, citation coverage, access denials, errors, and observability; and
- rebuild, rollback, revocation, and incident response expectations.

A small local, structured source set may need a compact documented review. A sensitive, multi-tenant, public, externally ingested, or action-taking context requires a deeper threat, privacy, and operational review. Guidance alone does not grant access to restricted evidence.

## Verification: Prove Use and Rejection

Grounding verification must include positive and negative cases. A system that finds an expected document but accepts the wrong one has not passed.

| Test class | Expected evidence |
| --- | --- |
| Correct retrieval | Uses the permitted canonical source and supports the stated claim with a valid citation or receipt. |
| Excluded/wrong-source rejection | Rejects an excluded, sibling, archived, unrelated, or lower-authority source even when it appears relevant. |
| Conflicting-source handling | Applies the documented authority rule or stops and surfaces an unresolved conflict. |
| Stale-context detection | Detects a changed, expired, or checksum/version-mismatched source and blocks or limits use as specified. |
| Citation integrity | Links claims to the correct canonical source and does not represent derived material as canonical evidence. |
| Prompt-injection resistance | Treats untrusted source text as data and does not follow embedded instructions that alter scope, policy, or permissions. |
| Containment and permissions | Enforces source/path/tenant boundaries and rejects unauthorized access or disclosure. |
| Rebuild and rollback safety | Shows that derived artifacts can be rebuilt from canonical sources, invalidated on change, and rolled back without changing source authority. |

Record fixtures, expected outcomes, results, and limitations in verification evidence. Test evidence should include both correct behavior and the rejected case that proves the boundary is real.

## Retrieval Posture

Do not make vector or semantic search the default. For a small, structured, high-consequence source set, use a deterministic source map and explicit authority rules first because they are easier to inspect, contain, and test.

Introduce semantic retrieval only after a demonstrated discovery problem shows that deterministic mapping is insufficient. The proposal must preserve the context contract, canonical-source verification, exclusions, permissions, citations, negative tests, rebuild/rollback evidence, and proportional security review. Better recall does not weaken the evidence boundary.

## Lifecycle Impact

Grounding governance extends the normal lifecycle; it is not a parallel process:

| Lifecycle point | Required grounding work |
| --- | --- |
| Intake and durable memory | Identify the supported decision, permitted evidence, forbidden uses, owners, and existing authority conflicts. |
| Specification | Define the full context contract, source authority, exclusions, failure behavior, and risk classification. |
| Build package | Bound the needed metadata, fixtures, permissions, observability, rebuild, rollback, roles, dependencies, and acceptance evidence. |
| Pre-code review | Red-team untrusted documents, prompt injection, stale/conflicting evidence, privacy, licensing, containment, and operational risk. |
| Implementation and verification | Preserve canonical/derived separation and test both approved retrieval and rejection behavior. |
| Deployment and operations | Authorize release separately; monitor source/index drift, citation coverage, retrieval errors, access denials, rebuilds, rollbacks, and retention obligations. |

Any material change to sources, authority, scope, access, retrieval approach, or risk reopens the affected artifacts, reviews, and gates.

## Writer's Studio Example

Writer's Studio is the concrete bounded-context example. Existing support includes source-bound manuscript sessions, explicit journal and continuity assets, checksums, stale-context blocking, and opt-in structured context records. Proposed but not implemented support includes a story/corpus registry, per-story source maps, and a read-only grounding audit.

The default policy is story-scoped context, not whole-vault grounding. A named story's active manuscript, journal, continuity assets, characters, and explicitly opted-in plot or lore may be permitted by its context contract. Archives, abandoned drafts, sibling stories, unrelated projects, PDFs, submissions, research, and prior AI/editor feedback remain excluded unless the contract explicitly admits them. Shared series canon is likewise an explicit opt-in source, never implicit whole-vault context.

## V1 Boundary

This guidance does not authorize provider calls, indexing, crawling, document storage, corpus-wide semantic search, source-material changes, or retrieval implementation. It supplies the governance and verification requirements a future project must satisfy before proposing those capabilities.
