# Dependencies

Skills in this repo that depend on external plugins. Install these before using `sdlc-orchestrator`.

## Required Plugins

### `superpowers` (by [obra](https://github.com/obra/superpowers))

Install inside Claude Code:

```
/plugin marketplace add obra/superpowers-marketplace
/plugin install superpowers@superpowers-marketplace
/reload-plugins
```

| Skill | Used In |
|-------|---------|
| `brainstorming` | P0 Ideation |
| `writing-plans` | P2 Architecture |
| `executing-plans` | P3 Execution |
| `test-driven-development` | P3 Execution |
| `using-git-worktrees` | P3 Execution |
| `dispatching-parallel-agents` | P3 Execution (parallel tasks) |
| `requesting-code-review` | P4 Validation |
| `receiving-code-review` | P4 Validation |
| `finishing-a-development-branch` | P5 Ship |
| `systematic-debugging` | P3/P4 failure handling |
| `verification-before-completion` | P3 task gates |

---

## Skills Provided by This Repo

These are bundled here — no separate install needed once you run `npx skills add github:Itskindastrange/sdlc-orchestrator`.

| Skill | Role in SDLC |
|-------|-------------|
| `sdlc-orchestrator` | Master orchestrator |
| `prd-writer` | P1 Product requirements |
| `design-doc-writer` | P2 Architecture / EDD |
| `qa-plan-writer` | P4 QA planning |
| `devils-advocate` | Gates across all phases (WAIM, Steelman, Brutal Mode) |
| `compact` | Session handoff at phase close |
