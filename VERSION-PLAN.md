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

### `v0.5.0-presentation-pass`

Focus:

- richer showdown visuals
- emoji system expansion
- card movement / reshuffle polish

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
