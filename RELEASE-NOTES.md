# Aegis v2.1.0 release notes

The stable Codex invocation is `$aegis`; the picker displays **Aegis v2.1.0**. This source release does not install or activate the skill on your system.

## Changes

- One canonical `skill/aegis` package, with versioned metadata and a full-package replacement path rather than parallel versioned invocation names.
- One risk-and-control matrix and one compact run brief for eligible reversible internal work, with a named implementer and linked results. Public-facing work retains at least standard controls, and sensitive work retains its applicable higher safeguards.
- A clear split between approved requirements, observed source facts, frozen plans, and append-only receipts. A small rebuild does not give the PM authority without explicit delegation.
- Shared elapsed-time and retry bounds, observable usage limits where applicable, and explicit stop and continuation rules. Stricter owner review requirements still apply.
- Separate decisions for candidate push/PR, CI effects, merge, promotion, and closure. Promotion requires owner approval before the action that triggers it.
- Published v2 behavior for intended RED then unchanged GREEN on executable fixes/features, and pass-before/pass-after with unchanged checks on behavior-preserving refactors. The [calculator baseline](examples/calculator/calculator-create.md) and [percent enhancement](examples/calculator/calculator-percent.md) retain their calculator behavior and verification expectations; their opening lines now use `$aegis` and verify the version and source.

## Validation and distribution

This release changes workflow guidance and package identity, not runtime enforcement. Both calculator prompts passed owner acceptance before the stable-name change. Fresh calculator runs, native discovery, live CI, and timing or false-stop measurements were not verified for this version. No new model router, sandbox, installer, runtime, dependency, or paid integration is included. The Hermes port is not included.

Follow the [README upgrade steps](README.md#install) to replace the entire package in the single active slot. Previous releases remain available in GitHub history.
