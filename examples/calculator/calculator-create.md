# Calculator baseline prompt

Paste this into a fresh Codex session started in your chosen empty project directory. Use the same prompt in PowerShell and WSL, each in a separate project folder. This prompt does not choose a machine-specific output path.

```text
Use $aegis. Before writing files, report the loaded skill name and metadata version (expected: aegis, 2.1.0), its actual source, current working directory and writable workspace. If that exact name, version and intended source cannot be verified, stop and report why; do not silently substitute another version. Keep all project artifacts and scratch output inside the current project. Do not inspect credentials or unrelated projects.

Build a polished, fully functional, single-page HTML/JavaScript calculator. This is a local offline baseline test, not a public service.

Specification:
- Deliver one self-contained index.html with inline CSS and JavaScript, no external dependencies, CDNs, network calls, telemetry, accounts or backend.
- Support addition, subtraction, multiplication, division, equals, decimal entry, sign toggle, clear and backspace.
- Use a readable display and visually distinct operator/action buttons. Make the layout responsive for desktop and a narrow mobile viewport.
- Support mouse, touch and keyboard: digits, decimal point, arithmetic operators, Enter or = for equals, Escape for clear, Backspace for deletion. Do not intercept browser shortcuts or trap keyboard focus. Show visible focus and meaningful accessible button labels.
- Define deterministic behavior for chained operations, repeated equals, starting a new entry after equals, leading zeros, repeated decimal points and incomplete expressions. Document those decisions before implementation; prefer the simplest sufficient behavior.
- Division by zero or invalid input must produce a recoverable error state, never crash. Clear restores normal operation. Document display precision and rounding; do not claim exact arbitrary-precision arithmetic.
- Exclude percent, history, scientific functions, themes/settings, persistence, deployment and packaging tools from this baseline.

Use Aegis's risk-proportionate lifecycle. Create or validate the single master spec.md and a bounded run-specific build package before implementation. I delegate routine in-scope isolated development decisions to the PM for this run, including plan and execution approval after the required review. Keep the PM non-implementing and obtain the independent checks required by Aegis. No authority to spend, install software, change security settings, publish, commit or modify outside this directory is delegated.

Target a 30-minute iteration. If the target is exceeded, record why, remaining work and the smallest recovery; do not expand scope or silently reduce acceptance criteria.

Write meaningful arithmetic and interaction checks before implementation where practical, show genuine feature failures then passing results, and test keyboard handling and responsive layout in a browser if available. Do not turn a missing browser into a pass or weaken its sandbox. Report unavailable checks and any human assistance precisely.

At closeout provide: how to open the calculator, files created/changed, tests and outcomes, gate decisions and approver evidence, limitations, elapsed time if measured, and the actual model/effort only if exposed by the host. Do not invent metrics. Leave the application ready for my manual acceptance, with no commit, deployment or push.
```
