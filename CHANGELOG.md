# Changelog

All notable iteration milestones for the CE demo live here.

## Unreleased

- Pending next milestone work after `v0.3.0-baseline`

## v0.3.0-baseline - 2026-04-05

### Added
- Rule debug scenario framework in `demo.html`
- Consolidated side panels and central table layout iteration
- Showdown hand-float / emoji reaction system
- Deck / discard pile visualization refresh
- Discard visibility model: face-up / face-down / destroyed count
- Discard tooltip sorting and recovery / reshuffle card-flight effects

### Fixed
- Showdown contestant eligibility now consistently excludes eliminated players
- Multi-step cover / raise reaction flow was hardened
- Several skill branches that could freeze the turn were repaired
- Surviving players no longer incorrectly lose number cards at stage transition

## Versioning Rules

- `major`: rules or architecture change in a way that breaks previous assumptions
- `minor`: a clear feature milestone or stable gameplay iteration
- `patch`: bug fixes, UI polish, animation tuning, wording adjustments

Example:
- `v0.4.0` discard pile system milestone
- `v0.4.1` discard tooltip polish
- `v0.4.2` discard-related bug fixes
