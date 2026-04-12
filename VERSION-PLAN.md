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

- `版本专题/v0.5.0-card-presentation-pass.md`
- `版本专题/v0.5.0-effect-layering-workplan.md`

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

- `版本专题/v0.6.0-ai-strategy-implementation-plan.md`

### `v0.7.0-ai-balance-pass`

Focus:

- add a guided new-player onboarding path before deeper balance work
- turn the shared AI engine into a more human-readable live-play opponent set
- connect strategy lab and balance lab back into real table pacing and result quality
- reduce "correct but stiff" decisions in cover / raise / hold / all-in timing
- keep `v0.6` settlement presentation stable while improving match readability and AI personality contrast

Planned workstreams:

- new-player onboarding entry on the start screen, with a guided 10-minute first-play path
- tutorial-specific explanation layers for win condition, round structure, cover/fold/all-in choices, and settlement
- AI live-play balance pass for `你 + 4AI`, especially mid-strength pressure, gold discipline, and over-cover behavior
- stronger persona separation in practical matches instead of only lab-side score differences
- in-match AI intent / risk readability, so players can more easily understand why an AI is pressing, holding, chasing, or folding
- simulation review pass to turn `ai_balance_lab` into a real regression gate before release

Success bar:

- a brand-new player can understand the game goal and one full round chain within about 10 minutes
- live matches feel less random and less samey across the four AI seats
- `ai_strategy_lab` choices better match what the same persona does in real games
- `ai_balance_lab` can surface obvious outliers before manual playtests
- no regression in start screen, showdown, settlement, or versioned test scenes

Reference:

- `版本专题/v0.7.0-ai-balance-pass.md`
- `版本专题/v0.7.0-new-player-onboarding-plan.md`

### `v0.7.5-skill-effect-pass`

Focus:

- run a large-scale skill-effect correctness and expectation-alignment sweep after repeated live-play findings
- fix places where actual release results differ from the original design intent for active skills, traps, and passive-linked effect chains
- improve card-by-card reproducibility through better test scenes before the next larger milestone continues
- keep the already-accumulated `v0.7.0` readability and AI work stable while the card-effect layer is corrected

Planned workstreams:

- build an “expected effect vs current runtime result” audit list for representative cards
- prioritize high-frequency, high-visibility, and high-impact skill mismatches first
- review release timing, target scope, card movement, gold movement, discard / recover chains, and public-card interaction rules
- unify card-effect validation through dedicated debug scenes instead of relying only on full-match replay
- convert the final fix list into a clean publishable update summary for GitHub-side release notes

Success bar:

- the most-played and most-visible skill / trap chains match their intended design in repeated playtests
- no obvious mismatch remains in core effect families such as draw, discard, recover, freeze, steal, public-card replace, or trap interception
- effect fixes can be reproduced from test scenes without replaying an entire live match each time
- `demo.html` stays syntax-clean and no blocker regression is introduced into the main live table flow

Reference:

- `版本专题/v0.7.5-skill-effect-pass.md`

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
