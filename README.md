# sdlc-orchestrator

The **SDLC orchestrator** skill cluster for Claude Code — drives a feature from idea → PRD → architecture → execution → QA → ship, triggering the right skill at each phase.

## Install

### Step 1 — Install the `superpowers` dependency

This cluster depends on [obra/superpowers](https://github.com/obra/superpowers). Install it first, inside Claude Code.

Register the marketplace:

```
/plugin marketplace add obra/superpowers-marketplace
```

Install the plugin:

```
/plugin install superpowers@superpowers-marketplace
```

Reload plugins:

```
/reload-plugins
```

### Step 2 — Install this plugin

In your terminal:

```bash
npx skills add github:Itskindastrange/sdlc-orchestrator
```

When prompted to choose which skills to install, press **spacebar** to select, and select **all** of them.

> **Tip:** if you have multiple AI agents installed (Claude Code, Cursor, Copilot), the installer may default to the wrong one. Force Claude Code explicitly:
> ```bash
> npx skills add github:Itskindastrange/sdlc-orchestrator --agent=claude-code
> ```

### Step 3 — Verify

Open Claude Code and check these skills are listed:

- From this repo: `sdlc-orchestrator`, `prd-writer`, `design-doc-writer`, `qa-plan-writer`, `devils-advocate`, `compact`
- From superpowers: `brainstorming`, `writing-plans`, `executing-plans`, `test-driven-development`, `finishing-a-development-branch`

Quick smoke test — start a new chat and say: `"let's build a new feature"` → `sdlc-orchestrator` should trigger.

> Full dependency breakdown: see [DEPENDENCIES.md](./DEPENDENCIES.md)

---

## Troubleshooting

**Skills installed but not showing up in Claude Code?**

If `npx skills add` ran but `sdlc-orchestrator` and friends don't appear, the installer likely mapped them to a different agent (Cursor, GitHub Copilot) instead of Claude Code.

**1. Diagnose — see where the skills landed and which agent they were assigned to:**

```bash
npx skills list
```

If you see `Agents: GitHub Copilot` (or anything other than Claude Code) next to your skill path, migrate the files manually.

**2. Migrate to the Claude skills directory:**

macOS / Linux:

```bash
mkdir -p ~/.claude/skills
mv ~/.agents/skills/* ~/.claude/skills/
```

Windows (PowerShell):

```powershell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.claude\skills"
Get-ChildItem -Path "$env:USERPROFILE\.agents\skills\*" | Move-Item -Destination "$env:USERPROFILE\.claude\skills\" -Force
```

**3. Restart Claude Code** — it won't discover the folders while running:

1. Type `exit` in the active Claude Code session.
2. Restart with `claude`.
3. Type `/` and confirm `sdlc-orchestrator` now appears in the completion menu.

**Prevent it next time** — target Claude Code explicitly on install:

```bash
npx skills add github:Itskindastrange/sdlc-orchestrator --agent=claude-code
```

---

## Skills (bundled in this repo)

### `sdlc-orchestrator`
Master workflow orchestrator. Routes through product → architecture → execution → validation → ship phases. Supports forward mode (greenfield), reverse mode (existing code, missing docs), and resume mode (pick up mid-chain).

### `prd-writer`
Write a PRD (Product Requirements Document) for any feature. Commits a `.md` file to the repo.

### `design-doc-writer`
Write an Engineering Design Doc (EDD). Documents architecture, schema, API contracts. Requires a PRD to exist first.

### `qa-plan-writer`
Write a QA Plan covering test strategy, test cases, and coverage targets. Requires PRD and/or EDD.

### `devils-advocate`
Multi-mode critical-thinking skill: WAIM (What Am I Missing?), Steelman, Standard 8-lens, 10x This, ELI5, Brutal Mode. Powers the gates between phases.

### `compact`
Trigger with the word `COMPACT` — summarizes the conversation into a structured handoff brief at each phase close.

---

## SDLC Phase Map

| Phase | Skills Used | Source |
|-------|-------------|--------|
| P0 Ideation | `brainstorming` | superpowers |
| P1 Product | `prd-writer` | **this repo** |
| P2 Architecture | `design-doc-writer`, `writing-plans` | this repo + superpowers |
| P3 Execution | `executing-plans`, `test-driven-development`, `using-git-worktrees`, `dispatching-parallel-agents`, `verification-before-completion` | superpowers |
| P4 Validation | `qa-plan-writer`, `requesting-code-review`, `receiving-code-review` | this repo + superpowers |
| P5 Ship | `finishing-a-development-branch` | superpowers |
| All phases | `devils-advocate` (gates) | **this repo** |
| Failure handling | `systematic-debugging` | superpowers |
| Session close | `compact` | **this repo** |

**Bundled here:** sdlc-orchestrator, prd-writer, design-doc-writer, qa-plan-writer, devils-advocate, compact

**Install separately via `superpowers`:** brainstorming, writing-plans, executing-plans, test-driven-development, using-git-worktrees, dispatching-parallel-agents, requesting-code-review, receiving-code-review, finishing-a-development-branch, systematic-debugging, verification-before-completion

---

## Structure

```
sdlc-orchestrator/
├── .claude-plugin/
│   └── plugin.json         ← plugin metadata + dependency declarations
├── skills/
│   ├── sdlc-orchestrator/SKILL.md
│   ├── prd-writer/SKILL.md
│   ├── design-doc-writer/SKILL.md
│   ├── qa-plan-writer/SKILL.md
│   ├── devils-advocate/SKILL.md
│   └── compact/SKILL.md
├── DEPENDENCIES.md
└── README.md
```

---

## Contributing

This project is **open source and open for contribution**. The workflow is a work in progress — feedback, fixes, and ideas are all welcome.

Found a bug, a rough edge, or have an idea to make the SDLC flow better?

- **Open an issue** — [github.com/Itskindastrange/sdlc-orchestrator/issues](https://github.com/Itskindastrange/sdlc-orchestrator/issues)
- **Send a pull request** — fork, branch, change, PR
- **Reach out directly** — abdullahahmaddd789@gmail.com

I'm actively looking to improve this workflow, so don't hesitate to suggest changes — big or small.

## Support

If this saved you time or made your build process cleaner:

- ⭐ **Star the repo** — it helps others find it
- 🔁 **Share it** with other Claude Code users
- 💬 **Tell me what worked and what didn't** — real usage feedback is the most valuable thing you can send

Thanks for checking it out.

---

## Credits

- **`devils-advocate`** is based on the original skill by **[Jean Kang](https://www.linkedin.com/in/advicewithjean)**, modified and extended here with additional sub-modes and personal workflow tweaks. Full credit to Jean for the original concept and design.
- **`superpowers`** (a runtime dependency, not bundled here) is by **[obra / Jesse Vincent](https://github.com/obra/superpowers)**.

## License

MIT — free to use, modify, and share.

Most skills in this repo are original work; `devils-advocate` is a derivative of Jean Kang's skill (see Credits). The `superpowers` plugin is a separate project by [obra](https://github.com/obra/superpowers), under its own license.
