# Changelog

All notable iteration milestones for the CE demo live here.

## v0.7.5 - in progress

- Branch focus: `v0.7.5-skill-effect-pass`
- Current focus:
  - Start a dedicated skill-effect correction pass after repeated live playtests exposed gaps between intended design and actual runtime behavior
  - Treat this version as a large-scale effect-quality and rules-alignment sweep instead of a broad new-feature release
  - Separate `v0.7.5` clearly from the already-accumulated `v0.7.0` readability / balance / UI optimization work
  - Prioritize high-frequency and high-impact active skills, traps, and passive-linked effect chains before opening new content
- Initial work plan:
  - Build a card-by-card audit list for “expected effect vs current runtime result”
  - Review release timing, target rules, draw / discard / recover / freeze / steal / public-card manipulation chains
  - Fix the most visible mismatches first, especially cases discovered through repeated real matches rather than only lab scenes
  - Expand existing test scenes so important skill-effect chains can be reproduced directly without replaying whole matches
  - Keep output grouped into a publishable fix summary for the later GitHub update

## v0.7.0 - release wrap-up

- Branch focus: `v0.7.0-ai-balance-pass`
- Status:
  - The main `v0.7.0` optimization batch is now in release-wrap-up state and ready for GitHub-side整理 / 归档 before the next version line continues
- Current focus:
  - Move the first `v0.7` slice to new-player onboarding, so a fresh player can understand the goal and full loop in about 10 minutes
  - Start the post-`v0.6` optimization cycle around AI live-play quality, persona contrast, and balance validation
  - Use `ai_strategy_lab` and `ai_balance_lab` as the primary review loop before pushing more visual or content-heavy work
  - Improve how clearly real matches expose AI intent, pressure timing, gold discipline, and chase risk
  - Keep the already-released settlement / showdown presentation stable unless a balance pass exposes a real gameplay regression
- Initial work plan:
  - Add a dedicated tutorial start entry on the start screen instead of forcing new players straight into the full live build
  - Define the minimum rules a new player must know: win condition, round flow, cover/fold/all-in choices, and settlement logic
  - Build a guided first-play script that teaches one complete round chain through controlled states and UI highlights
  - Compare lab decisions against real-table behavior for `老李A / 小美B / 阿杰C / 大伟D`
  - Identify the highest-value AI issues in over-covering, passive hold, weak all-in timing, and mid-strength pressure spots
  - Tighten persona-specific thresholds so expert / veteran / steady / aggressive players stop collapsing into one shared rhythm during long matches
  - Turn `ai_balance_lab` into a repeatable release gate for future `v0.7` checkpoints

## v0.6.0 - 2026-04-10

- Branch focus: `v0.6.0-ai-strategy-pass`
- Current progress:
  - Added a first-pass advanced AI lane for `阿杰C`, the current strongest AI sample
  - `aiAction(idx)` can now route `阿杰C` into a shared-context strategic path instead of the old random-weighted branch
  - Added `buildAIContext(idx)` and supporting helpers so the AI can reason about current hand rank, target hand, gap, public cards, target opponents, and current school investment
  - First-pass strategic logging now records scans such as `牌型扫描 / 技能决策 / 盖牌决策 / 初始被动 / 淘汰被动 / 回合升级`
  - Initial passive selection, elimination passive selection, per-turn skill upgrade, and elimination upgrades have all started using the same advanced scoring path for `阿杰C`
  - `阿杰C` now begins choosing passives and upgrades based on resonance chase, economy pressure, search support, hand pressure, and current plan fit instead of fixed random-first picks
  - Added an opponent-behavior memory layer for `阿杰C`, so it can remember recent average cover counts, raise rate, fold rate, and check rate per opponent
  - Added first-pass pot-odds and table-pressure reasoning to `阿杰C`, so cover / hold / raise / fold decisions now compare estimated win rate against current required rate instead of relying only on hand rank and gap-to-plan
  - Added first-pass bluff / anti-bluff logic to `阿杰C`, so it can selectively apply pressure on soft tables and call or raise lighter against suspiciously over-covered opponents
  - Added a dedicated `ai_strategy_lab` scenario and `🧠 AI测试台`, with fixed states for strong value pressure, search-first play, bluff pressure, anti-bluff follow-up, negative-EV fold, and early-round hand accumulation checks
  - Added a first-pass scene-driven focus layer for `阿杰C`, so it can distinguish between `强牌施压 / 成牌兑现 / 追牌 / 收紧保金 / 存牌爆发 / 反诈唬`
  - Added an in-panel AI decision breakdown for `ai_strategy_lab`, so current hand, target hand, focus, strongest read, chosen skill/trap, and cover action can be checked without only reading the raw logs
  - Advanced skill target choice is now in a first-pass scored state, so `夺取金币 / 夺取手牌 / 压制弃牌 / 查看盖牌 / 冻结盖牌` no longer default to random targets and instead factor in current resources, pressure baselines, bluff signals, and persona biases
  - Upgrade investment timing now uses first-pass momentum scoring, so recent successful skills, chase focus, pressure focus, search bias, and school / resonance synergy all influence whether `阿杰C` upgrades now or holds gold
  - `老李A` now shares the same advanced AI engine through an `经验型` parameter layer instead of staying on the old random-weighted branch
  - `ai_strategy_lab` now includes both `阿杰C（精算型）` and `老李A（经验型）` presets, making it easier to compare “same situation, different personality” behavior directly in the lab
  - `ai_strategy_lab` is now grouped inside one unified AI testing scene, with separate `行动决策` and `升级投资` preset sections instead of forcing review across multiple scattered labs
  - Added dedicated upgrade-investment presets for both `阿杰C` and `老李A`, so search-upgrade, synergy-upgrade, economy-upgrade, and disciplined hold-gold decisions can be reviewed from the same AI testing entry point
  - `ai_strategy_lab` now exposes an upgrade-investment breakdown panel, so AI upgrade decisions can be inspected as `基础分 / 场景加成 / 协同加成 / 动量加成 / 投资约束` instead of a single summary sentence
  - Advanced target scoring now applies per-persona weights for resource denial, growth threat, exposure threat, bluff discount, and search/public/swap preferences, so `阿杰C` and `老李A` no longer share the same target logic under different labels
  - Bluff evaluation now estimates per-target fold chance and surfaces `关键阻挡者`, instead of relying only on one table-average bluff number
  - Chase confidence now discounts only against **visible** discard dead-outs, matching the human information model where dark discard and destroyed cards stay hidden
  - Recent search-skill usage now feeds into bluff / anti-bluff reads, so both self-image and opponent reads can treat repeated search actions as stronger “real hand” signals
  - `小美B（稳健型）` and `大伟D（激进型）` now also share the same advanced AI engine, extending the lab from two sample personas to four
  - `ai_strategy_lab` now includes fixed action and upgrade presets for all five AI personas, so decision style differences can be compared inside one testing scene
  - Added `思思E（新手保守型）` as a simulation-only fifth AI persona for strategy lab and future balance simulations, without changing the live playable roster from `你 + 4AI`
  - `ai_strategy_lab` now covers five AI personas across action and upgrade presets, making it possible to compare expert, veteran, steady, aggressive, and novice-cautious behavior in one scene
  - Persona-specific tuning now also drives focus competition, skill taste, pressure thresholds, and upgrade thresholds, so the five AIs diverge in actual behavior instead of only sharing different labels
  - `ai_strategy_lab` now surfaces a `焦点竞争` breakdown, making it easier to inspect why one persona chooses `强牌施压`, `追牌`, `收紧保金`, or `存牌爆发` in the same situation
  - Added `ai_balance_lab`, a simulation-only 5-AI auto-run / balance test entry that keeps the live playable roster unchanged while letting `思思E / 老李A / 小美B / 阿杰C / 大伟D` run repeated pure-AI matches for win-rate, average-rank, average-chip, DJ-entry, and recent-match summaries

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
  - Passive / resonance labs now expose fuller preview coverage, and missing runtime result layers such as `扩容背包 / 迷雾降临 / 永冻力场 / 尸体收益` now also show clearer draw, public-cover, freeze, and gain feedback
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
- `v0.6.0-ai-strategy-pass`
  - 开始定向重塑阿杰C：降低多人局中的反制/找牌过度投入，提高成牌兑现、收割目标选择与中强牌主动施压倾向，不调整老李A。
