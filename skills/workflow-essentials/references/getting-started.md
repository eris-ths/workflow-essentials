# Getting Started

## Installation

1. Add workflow-essentials as a Claude Code plugin to your project
2. Start using commands immediately — no configuration needed

## Your First Session

```
1. /ctx                    ← Check if there's a previous session to resume
2. [do your work]
3. /devil                  ← Review your changes before committing
4. /ship                   ← Commit (and optionally deploy)
5. /ctx save               ← Save your session state for next time
```

## Tips

### Start with /devil

If you only use one command, make it `/devil`. It catches bugs and security issues before they ship. The convergence principle (fix → re-review → repeat until zero concerns) ensures nothing slips through.

### /ctx is your memory

Claude Code sessions are ephemeral. `/ctx save` at the end of each session creates a breadcrumb trail. `/ctx` at the start picks it up.

### Configure /ship for your project

Without `.claude/ship.yml`, `/ship` will:
- Run `/devil` (always)
- Skip tests (no test command configured)
- Commit with conventional commit format
- Skip deploy (no deploy command configured)

Add a `ship.yml` to unlock the full pipeline.

### /reflect is optional but compounds

Each `/reflect` entry is a gift to your future self. Over time, MEMORY.md becomes a project-specific knowledge base that Claude Code reads automatically.
