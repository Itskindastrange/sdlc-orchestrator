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

### Step 3 — Verify

Open Claude Code and check these skills are listed:

- From this repo: `sdlc-orchestrator`, `prd-writer`, `design-doc-writer`, `qa-plan-writer`, `devils-advocate`, `compact`
- From superpowers: `brainstorming`, `writing-plans`, `executing-plans`, `test-driven-development`, `finishing-a-development-branch`

Quick smoke test — start a new chat and say: `"let's build a new feature"` → `sdlc-orchestrator` should trigger.

> Full dependency breakdown: see [DEPENDENCIES.md](./DEPENDENCIES.md)

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
