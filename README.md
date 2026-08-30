# Aegis

![Aegis: Build with AI. Decide with confidence.](assets/aegis-hero-v2.png)

Aegis is a Codex skill for planning and building software with clear scope,
risk-aware checks, human approval, and useful evidence.

## Install Aegis

Aegis is installed as a Codex skill. The complete skill is in the `skill/aegis`
folder of this repository. Keep the folder together; it contains `SKILL.md`,
`agents`, and `references`.

### Choose where to install it

| If you want Aegis to be available... | Install the folder here |
| --- | --- |
| In all of your local Codex projects | `~/.agents/skills/aegis` |
| In one repository | `<repository-root>/.agents/skills/aegis` |

On Windows, the personal location is
`%USERPROFILE%\.agents\skills\aegis`.

### Download and install

1. Open the [Aegis repository](https://github.com/dotnetdavid/aegis).
2. Download the repository as a ZIP file, or clone it with Git.
3. Open the downloaded repository and find `skill/aegis`.
4. Copy the complete `aegis` folder to the location you chose above.
5. Confirm that the installed folder contains `SKILL.md`, `agents`, and
   `references`.

## Start using Aegis

1. Start a new Codex session.
2. Type `$aegis` in your request.
3. Tell Codex what you want to build, change, or review.

For example:

```text
$aegis Help me plan this project. Start by asking what outcome we need and
what constraints matter before proposing implementation work.
```

Aegis will ask focused questions and guide the work according to its risk.
You remain responsible for the decisions and approvals.

## If Aegis does not appear

Check that the final folder path is exactly one of these:

- `~/.agents/skills/aegis`
- `<repository-root>/.agents/skills/aegis`
- `%USERPROFILE%\.agents\skills\aegis` on Windows

The folder should contain `SKILL.md` directly, not another nested `aegis`
folder. Then start a new Codex session.
