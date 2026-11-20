# Aegis v2.1.0: Leaner and Meaner

![Aegis: Build with AI. Decide with confidence.](assets/aegis-hero-v2.png)

Aegis helps an AI coding assistant turn an idea into bounded work, tested changes, and reviewable decisions. Use `$aegis` in Codex; the version is shown separately as **Aegis v2.1.0**.

## How it works

The PM coordinates scope, requirements, delegation, evidence, and communication without implementing product changes. For eligible reversible internal work, use one compact run brief and linked results. Name the human implementer or one bounded delivery agent. Public-facing work retains at least standard controls; security, privacy, and other higher-consequence work retains its applicable safeguards. Independent review remains independent of the PM.

Each governed project has one current `spec.md`. Code and observed checks show what exists; the approved spec defines what is required. Freeze the run plan and record approvals, reviews, and results in dated receipts only after they occur. Set time and retry bounds before work and hold when capacity or authority cannot be verified.

New executable behavior and fixes require intended RED before edits and GREEN with the unchanged checks afterward. Behavior-preserving refactors require a passing baseline and the same passing checks afterward. A failed baseline blocks the refactor path.

The nine gates remain: scope, build package, pre-code review, execution authorization, acceptance, commit, deployment, post-deployment acceptance, and push/PR/closeout. Authorize actions according to what they actually do. For example, approving a candidate PR does not authorize its CI effects, merging it, or deploying it.

Aegis is guidance, not a sandbox, permission system, or enforcement engine. Host permissions and human review still matter.

## Install

To install, put the complete `skill/aegis` folder, including `agents` and `references`, in one discovery location: normally `~/.agents/skills/aegis` (personal) or `.agents/skills/aegis` in the relevant repository. Do not install duplicate active copies. Publishing these files does not install or replace a local skill.

Use one active `aegis` slot. A `git pull` updates the installed package only if Codex discovers the tracked folder from that checkout, directly or through an existing supported link. If Codex uses a separately copied package, replace the entire installed folder from the intended release; do not merge old and new files.

1. Stage and verify the intended release outside live discovery. Check the complete package, expected version and source; use a truly isolated Codex environment if testing discovery before cutover.
2. Close affected Codex sessions before modifying the active discovery locations. After the owner approves the exact locations, replace the complete package in the existing slot. If migrating from `aegis2`, retire only the approved legacy slot before exposing the new one. Never make both slots discoverable at once.
3. In a fresh Codex session, confirm that exactly one active `aegis` entry resolves to the intended source and version. If verification fails, stop using the skill and restore the intended prior release from GitHub into the single active slot, with approval for the affected location. Do not keep a second active copy or a local rollback copy.

Windows PowerShell and WSL are separate hosts. In a fresh Codex session, confirm the loaded skill name, metadata version, actual source, working directory, and writable scope before any writes. Do not run the examples in a credentials directory.

## Getting started: calculator demo

1. In an empty, isolated project folder, invoke `$aegis` and paste the text block from the [baseline prompt](examples/calculator/calculator-create.md).
2. Review and accept the baseline before pasting the [percent prompt](examples/calculator/calculator-percent.md) into the same project. Keep the original regression checks.
3. Keep all project output in the isolated folder. Neither example requires a commit, deployment, or publication.

## Validation and limits

Both calculator examples passed owner acceptance before the stable-name change using session-local guidance. That did not verify native skill discovery or the installed source under the stable name. Native discovery, a fresh calculator rerun, live CI, and timing or false-stop measurements are not verified for this version.

See [release notes](RELEASE-NOTES.md) for scope and release boundaries.

## Creator and license

Created by David A. Frey.

Copyright (c) 2026 David A. Frey. Licensed under the [MIT License](LICENSE). Keep the copyright and permission notice with copies or substantial portions.
