# Percent enhancement prompt

Run this in the existing calculator project after completing and accepting the baseline. Use the same prompt for independent PowerShell and WSL projects.

```text
Use $aegis to enhance this existing calculator. Before writing files, report the loaded skill name and metadata version (expected: aegis, 2.1.0), its actual source, actual project directory and writable scope. If that exact name, version and intended source cannot be verified, stop and report why; do not silently substitute another version. Read the current master spec.md, prior acceptance and test evidence. Preserve baseline records and unrelated changes. Keep all new output inside this project.

Add one percent button and keyboard % support. Define percent as a unary operation: divide the currently displayed operand or result by 100. It is not context-sensitive retail-calculator percentage behavior.

Required acceptance:
- 5 then % displays 0.05.
- 50 * 5 % = produces 2.5.
- 200 + 10 % = produces 200.1, not 220.
- 0 % remains 0; -5 % produces -0.05.
- Repeating % applies division by 100 again.
- Applying % to a completed result operates on that result.
- Invalid/error state remains recoverable with clear.
- Mouse/touch and keyboard % give identical arithmetic semantics. Test the emitted % key or a physical Shift+Digit5 sequence as appropriate; diagnose harness mistakes separately from product defects.
- Existing operations, input handling, focus, accessibility and responsive layout continue working.

Keep the existing design coherent. No additional functions, dependencies, network use, persistent storage, broad refactor or unrelated redesign.

Amend the existing master spec.md for this requirement through the applicable Aegis gates; do not create a competing specification. Create a new run-specific build package and preserve prior evidence. I delegate routine in-scope isolated development decisions to the PM for this run, with required independent review/testing unchanged. No spending, software installation, security-setting changes, commits, deployment, publication or writes outside this directory are authorized.

Target 30 minutes. First demonstrate meaningful percent feature failures while original baseline cases still pass; then implement the smallest change and rerun both new cases and original regression cases against the final product. Keep failed evidence and document corrections. Run browser interaction checks if available; report any blocked tests or owner-run assistance honestly without bypassing protections.

Report changed files, actual test results, gate decisions, remaining limitations and measured time. Leave the result for manual acceptance without commit, deployment or push.
```
