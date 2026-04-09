# Version Plan

## Goal

Keep each playable milestone recoverable so we can:

- observe iteration quality over time
- rollback safely after risky changes
- isolate regressions faster

## Branch Strategy

### `main`

- Always represents the latest stable playable baseline
- Only merge in after a focused manual smoke test

### Feature Branches

Use one branch per larger topic:

- `codex/ui-discard-pile`
- `codex/showdown-presentation`
- `codex/rule-cover-chain`
- `codex/skill-passive-fixes`

## Tag Strategy

Create a tag for every milestone worth revisiting.

Recommended format:

- `v0.3.0-baseline`
- `v0.4.0-discard-pile`
- `v0.4.1-discard-polish`
- `v0.5.0-showdown-ui`

Rules:

- tag only after the version is playable
- tags should map to a specific reviewable milestone
- do not tag half-finished WIP states

## Commit Rhythm

For this project, prefer small grouped commits instead of giant dumps.

Recommended grouping:

1. layout / visual structure
2. rule logic
3. bug fixes
4. animation polish
5. docs / test scenarios

## Release Checklist

Before calling a version stable:

1. `demo.html` passes `node --check`
2. Start screen loads correctly
3. A normal game can complete at least one full turn chain
4. No obvious blocker in action / showdown / settlement flow
5. Changelog is updated
6. Tag name is decided before the release commit

## Current Suggested Milestones

### `v0.3.0-baseline`

Current stable baseline after:

- side panel consolidation
- central board re-layout
- showdown presentation pass
- debug scenario framework
- discard pile system pass

### `v0.4.0-rules-pass`

Focus:

- cover / raise / react chain
- showdown legality checks
- skill / passive timing fixes

### `v0.4.1-bugfix-pass`

Focus:

- system sweep for runtime blocker bugs
- showdown / resonance / discard-recovery stability
- player choice / modal / selection flow fixes
- continue validating bugfixes against live play sessions

### `v0.5.0-card-presentation-pass`

Focus:

- unified card presentation system
- skill / trap / passive / resonance card UI
- stronger cast / impact / result feedback
- first representative card batch integration

Status:

- first playable release completed as `v0.5.0`

Reference:

- `v0.5.0-card-presentation-pass.md`
- `v0.5.0-effect-layering-workplan.md`

### `v0.6.0-ai-strategy-pass`

Focus:

- land the shared AI decision engine for Step 1~5
- turn role docs into configurable player personas
- reduce random-only behavior in skill / cover / fold / upgrade choices
- prepare large-scale automated simulations for later balance work

Current progress:

- strongest sample `阿杰C` already uses the shared strategic lane
- `老李A / 小美B / 大伟D` now also share the same advanced AI engine through distinct persona layers
- `思思E` is now added as a simulation-only fifth AI persona for lab and future balance-simulation use, while the live playable roster remains unchanged
- opponent behavior memory and pot-odds reasoning are in place
- bluff / anti-bluff first pass is now wired into fixed lab states
- dedicated `ai_strategy_lab` is available for repeatable AI decision reviews
- `ai_strategy_lab` now covers all five AI personas across action and upgrade presets
- advanced target choice now uses persona-weighted scoring instead of one shared target heuristic
- bluff evaluation now estimates per-target fold chance and shows a `关键阻挡者` in the AI lab
- visible-discard dead-outs and recent search-skill image are now part of chase / bluff confidence
- `ai_balance_lab` is now in progress as the next-step 5-AI automated simulation and balance summary entry, using `思思E / 老李A / 小美B / 阿杰C / 大伟D` without changing the live playable `你 + 4AI` roster

Reference:

- `v0.6.0-ai-strategy-implementation-plan.md`

## Practical Workflow

Use this order every time:

1. create / switch to a feature branch
2. implement one contained milestone
3. run syntax check and manual smoke test
4. update `CHANGELOG.md`
5. merge to `main`
6. create a version tag

## Notes

- Do not duplicate the whole `demo.html` as manual backups
- Prefer `git commit + git tag` over `demo-v2.html` style snapshots
- If a change is risky, branch first even if it is only one file
