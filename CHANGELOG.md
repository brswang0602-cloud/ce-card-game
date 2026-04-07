# Changelog

All notable iteration milestones for the CE demo live here.

## v0.5.0 - 2026-04-08

- Release version: `v0.5.0`
- Focus: unified card presentation, card copy normalization, card-based selection / upgrade flows, and first-batch effect layering
- Release summary:
  - Skill / trap / passive / resonance presentation lanes now have dedicated test labs
  - Initial passive selection now supports a batch center reveal before cards fly to each player's passive area
  - Upgrade windows now preview the current effect by default and switch to upgraded effect on hover / selection
  - Hover tooltips now include shared keyword annotations for search / recover / seize / lose / pay / freeze / destroy
  - A first-batch `effect_layering_lab` now differentiates result-stage motions such as draw / discard / recover / freeze / steal / public-card replace
  - Representative runtime skills now route their result stage through differentiated motion layers instead of a single shared helper feel
  - Second-batch composite skills such as `潜流 / 资产查没 / 暗箱操作 / 战术校准 / 骨矛 / 尸骸拼凑` now also use layered result motions in both the lab and live skill resolution
  - Additional active skills such as `战术武装 / 鲜血交易 / 威压 / 寒潮` now use distinct skill-gain or pressure-style result feedback instead of generic shared helpers
  - Aura / stance-type actives such as `堡垒武装 / 加税令 / 瘟疫` now also participate in the same result-layering test lab and live resolution path
  - Result layering now adds zone-local pulses and more differentiated flight card styles for skill gain, recover, public-card replace, cover reinforcement, and aura pressure
  - Lab-only effect-layering previews such as `筛选 / 快速装填 / 降雨 / 威慑射击` are now fully hooked into live inline resolution, and steal/public/search flows have a clearer distinction via public-flight, steal-flight, hand-zone pulses, and discard-zone pressure
  - Judge, cleanse, recover, freeze, and corpse-style skills now also add clearer zone-local feedback so `幸运币 / 致命判定 / 提纯 / 鲜血交易 / 尸骸拼凑 / 冥界之门` no longer feel like the same generic shared result layer
  - Passive and resonance trigger lanes now start using the same result-layering system, so representative passive / resonance effects no longer stop at mini-card popups and can show actual gold, draw, recover, cover, and public-card result directions
  - Runtime passive / resonance triggers such as `帝国国库 / 严苛税法 / 水压充能 / 紧急变现 / 金权交易 / 黑暗仪式 / 亡灵天灾 / 战术口袋 / 左轮置换 / 绝对容积 / 走火 / 双发 / 亡者加护` now route their real trigger stage through layered result motions instead of old one-off helper flashes
  - All trap cards are now covered by four dedicated animation templates: counter intercept, cover ambush, skill rewrite, and showdown reversal
  - Trap labs now include skill smash, rewrite offset, judge-card reveal, and ambush emoji timing refinements
  - Debug labs now support pausing via Space or the pause button, so motion-heavy test scenes can be frozen for close inspection

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
