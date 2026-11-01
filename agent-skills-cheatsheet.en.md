# Agent Skills Cheatsheet

> Version v0.8 · Data as of 2026-11-01 · Covers 28 entries · Daily-updated guide to agent skills for Claude Code, Codex, Cursor, OpenCode, Gemini CLI and other coding agents

## How to read an entry

Every entry answers five questions in plain language:

- **What it does** — the problem it solves and the mechanism it uses, in one sentence. No marketing copy.
- **Form** — what you actually install: a *single skill* (one SKILL.md package), a *collection* (many skills/plugins in one repo), a *framework* (a system for organizing skills), a *scanner/directory* (safety tooling around skills), or a *creation tool* (makes new skills).
- **Works with** — the agents it is known to support, as stated by the source.
- **License** — the project's own license, where verified from the repo; "see repo" means not yet verified here.
- **Stars (snapshot)** — cumulative GitHub stars as reported by the source on the date in parentheses. A dated heat snapshot, not a live count and not a quality score.

## Quick picks by scenario

| Scenario | First pick | Why | Backups |
|---|---|---|---|
| Audit code your agent wrote | cloudflare/security-audit-skill | Six-stage audit with finder/verifier separation; built to kill false positives | NVIDIA/SkillSpector (scan the skill itself), SkillzBench (pre-scanned directory) |
| Your agent's UI looks like generic AI slop | Nutlope/hallmark | Purpose-built anti-slop design skill for the major coding agents | pbakaus/impeccable (design vocabulary + deterministic checks), Leonxlnx/taste-skill, heydamir/unslop (audit-then-redline pass by pass), Motionsites-AI/claude-skill (cinematic landing pages) |
| Make the agent write less, better code | DietrichGebert/ponytail | "Lazy senior engineer" style skill with measured code/time reductions | multica-ai/andrej-karpathy-skills (Karpathy's practices as one CLAUDE.md), mattpocock/skills (composable engineering-practice skills) |
| Scientific research with an agent | K-Dense-AI/scientific-agent-skills | 177 ready-made research skills + 100+ scientific databases | Graphify-Labs/graphify (turn your codebase into a queryable graph first) |
| Give non-coding roles their own agent setup | anthropics/knowledge-work-plugins | Anthropic's official role-based plugin templates (sales, legal, finance…) | cursor/plugins (Cursor's official catalog) |
| Turn a desktop app into something an agent can drive | HKUDS/CLI-Anything | Auto-generates a CLI harness + SKILL.md for arbitrary software | Microsoft Skill Recorder (capture a human doing it once) |
| Organize / tune many skills at once | affaan-m/ECC | Harness performance system spanning skills, memory, security | obra/superpowers (agent skills framework) |

## 🧑‍💻 Maintainer's own skills

Skills written by this cheatsheet's maintainer, Gamehu — listed separately from the collected entries below, and held to the same entry standard.

| Skill | What it does | Form | Works with | License | Stars (snapshot) | First collected |
|---|---|---|---|---|---|---|
| [Gamehu/wechat-mp-skill](https://github.com/Gamehu/wechat-mp-skill) | A WeChat Official Account publishing skill: converts Markdown into WeChat-compatible HTML and creates/manages articles in the account's draft box through the WeChat API, with the token-cache and dynamic-IP whitelist failure modes (errors 40164 / 40001) documented from daily production use — it formats the maintainer's three daily briefings for WeChat | Single skill | SKILL.md-based agents | No LICENSE file in repo | 0 (2026-10-30) | 2026-10-30 (in production use since 2026-09-28) |
| [Gamehu/reins](https://github.com/Gamehu/reins-en) | Three skills that keep a coding agent on the plan you approved: `spike-design` turns a requirement into a reviewable, code-free plan — goals and non-goals, a structure skeleton, and an abstraction/dependency budget that defaults to zero — cut into ~300-line slices with numbered decisions; `risk-walkthrough` then walks only the hard parts of each slice and labels every deviation "needs your decision" or "already in the plan"; `quality-review` re-checks plan vs code in a fresh context and reports without ever editing. No runtime, nothing to install. (English edition linked; a Chinese edition lives at Gamehu/reins.) | Collection (3 skills) | Claude Code, Codex, OpenCode | MIT | 0 (2026-10-30) | 2026-10-30 |

## 🔐 Security & auditing

Skills that audit agent output, and tooling that audits the skills themselves — the supply-chain layer of the skills ecosystem.

| Skill | What it does | Form | Works with | License | Stars (snapshot) | First collected |
|---|---|---|---|---|---|---|
| [cloudflare/security-audit-skill](https://github.com/cloudflare/security-audit-skill) | Turns a coding agent into a security auditor that works in six stages (recon → coverage-guided hunting → adversarial verification → structured output → independent re-check → neutral report), with finder and verifier kept separate so findings arrive with a full source trace instead of false-positive noise; Cloudflare runs it continuously over its own repos | Single skill | Coding agents (Claude Code class) | MIT | 55,407 (2026-11-01) | 2026-10-21 |
| [NVIDIA/SkillSpector](https://github.com/NVIDIA/SkillSpector) | Scans an agent skill *before you install it* for vulnerabilities, malicious patterns, prompt injection, data exfiltration and supply-chain risk — the pre-flight check for third-party SKILL.md files | Scanner | Claude Code, Codex, MCP skills | see repo | 22,164 (2026-10-27) | 2026-10-27 |
| [SkillzBench](https://signalnewsharrisonburg.com/press-releases/80473/skillzbench-launches-free-directory-that-security-scans-and-benchmarks-ai-agent-skills-before-agents-use-them/) | A free directory that security-scans every listed skill, benchmarks it with an A/B test (same model, with vs. without the skill, publishing the score delta — including negative ones), and serves your hand-picked set to your agent through an MCP connector | Directory + benchmark | Any agent via MCP | n/a (service) | n/a | 2026-10-26 |

## 🎨 Design & UI

Design skills exist because agent-generated interfaces converged on one generic "AI look". These give the agent a design vocabulary, a process, or explicit anti-slop rules.

| Skill | What it does | Form | Works with | License | Stars (snapshot) | First collected |
|---|---|---|---|---|---|---|
| [Nutlope/hallmark](https://github.com/Nutlope/hallmark) | An anti-"AI-slop" design skill: explicit rules and references that push a coding agent's front-end output away from the default gradient-and-glass look toward deliberate, product-specific design | Single skill | Claude Code, Cursor, Codex | MIT | 43,986 (2026-11-01) | 2026-10-25 |
| [pbakaus/impeccable](https://github.com/pbakaus/impeccable) | Gives a coding agent a shared design language: one `/impeccable init` writes the product facts into PRODUCT.md, 24 shared commands cover shaping, critique, polish and motion, and 61 deterministic checks run in the CLI or a browser extension without calling a model | Skill + command set | Coding agents (harness-level) | Apache-2.0 | 98,367 (2026-11-01) | 2026-10-27 |
| [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) | A ten-stage design-taste workflow for agents, gated by real-browser verification tests, so "looks right" is checked in an actual browser instead of asserted by the model | Single skill (workflow) | Coding agents | MIT | 105,615 (2026-10-30) | 2026-10-30 |
| [alchaincyf/huashu-design](https://github.com/alchaincyf/huashu-design) | An HTML-native design skill that returns deliverable design work from one prompt inside the agent — web/app prototypes, editable PPTX decks, animation and infographics — instead of a static mockup image | Single skill | Coding agents | see repo | 26,723 (2026-10-27) | 2026-10-27 |
| [elayadesign/ai-design-skills](https://github.com/elayadesign/ai-design-skills) | A growing collection of self-contained design skills for AI coding tools (starting with a landing-page skill covering intake questions, page structure, conversion copy and a full visual system), each installed as one folder the agent reads as a markdown rules file | Collection | Claude Code, Cursor, Codex, Windsurf, markdown-rules readers | MIT | 12,255 (2026-10-30) | 2026-10-29 |
| [heydamir/unslop](https://github.com/heydamir/unslop) | A single skill that audits a vibecoded screen for AI-slop markers (purple gradients, glows, emoji labels, shouty copy, uneven spacing), sets a design direction from the product, then fixes it pass by pass like a designer doing a redline review — and can render a short story video of the screen unslopping itself | Single skill | Claude Code | CC BY 4.0 | 3,598 (2026-11-01) | 2026-10-31 |
| [Motionsites-AI/claude-skill](https://github.com/Motionsites-AI/claude-skill) | A free Claude skill that builds cinematic, award-level landing pages: it matches the brief against 40 reference designs and a shelf of real hero media, writes a precise build spec, then screenshots its own output and fixes it against a QA rubric until it clears a gallery-level bar | Single skill | Claude Code, Claude.ai / Claude desktop | MIT for skill code; examples/media © MotionSites (use to build, not to resell/redistribute) | 1,299 (2026-11-01) | 2026-11-01 |

## 💻 Coding practice

Skills that change *how* the agent writes code — engineering judgment, house style and methodology, packaged as instructions the agent loads every run.

| Skill | What it does | Form | Works with | License | Stars (snapshot) | First collected |
|---|---|---|---|---|---|---|
| [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) | A "lazy senior engineer" persona skill that makes the agent write less code and verify more: measured on 39 tasks at −53% code volume, −41% time, with tests on 98% of high-risk logic; v5.3 adds a live cost/time/token band on top of Claude Code plus a local task board | Single skill | Claude Code | see repo | 169,603 (2026-10-21) | 2026-10-21 |
| [multica-ai/andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills) | Distills Andrej Karpathy's public observations on LLM coding pitfalls into a single CLAUDE.md skill file, so the agent inherits a well-known engineer's working rules without you writing them | Single skill (CLAUDE.md) | Claude Code | see repo | +3,286 in one week (2026-10-28) | 2026-10-26 |
| [mattpocock/skills](https://github.com/mattpocock/skills) | A collection of small, composable engineering-practice skills — requirements interviews, TDD red-green-refactor loops, systematic debugging, code review against the originating spec — that steer a coding agent without imposing an end-to-end process framework | Collection | Claude Code, Codex, GitHub Copilot, Gemini CLI | MIT | 306,678 (2026-10-30) | 2026-10-30 |
| [t3dotgg/tstack](https://github.com/t3dotgg/tstack) | Nine PR-workflow skills (full-send, council, sol-loop, takeover, babysit-pr…) that carry a code change from branch to merged PR — proving it, reviewing it across models from different providers, filing a short problem-led PR and babysitting it through CI — instead of stopping at the diff | Collection (9 skills) | Claude Code, Codex | MIT | 2,473 (2026-10-31) | 2026-10-31 |
| [github/lever](https://github.com/github/lever) | GitHub's official Copilot plugin that turns a vague complaint ("CI feels slow") into a Loop Card — the metric, how to measure it, how noisy it is and what counts as a win — so the agent can iterate against a number instead of your patience | Collection (plugin) | GitHub Copilot | MIT | 240 (2026-11-01) | 2026-10-31 |

## 🔬 Research & knowledge

Domain knowledge, packaged for agents — deep skill packs for a field, and tools that turn existing material into agent-queryable knowledge.

| Skill | What it does | Form | Works with | License | Stars (snapshot) | First collected |
|---|---|---|---|---|---|---|
| [K-Dense-AI/scientific-agent-skills](https://github.com/K-Dense-AI/scientific-agent-skills) | 177 ready-to-use scientific-research skills (biology, chemistry, medicine, drug discovery) wired to 100+ scientific databases, so a general agent can run domain workflows it was never trained for | Collection (177 skills) | Cursor, Claude Code, Codex; open Agent Skills standard | see repo | 53,576 (2026-10-22) | 2026-10-22 |
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | Converts a whole codebase — code, docs, SQL schemas, PDFs — into a queryable knowledge graph exposed as a `/graphify` skill; parsing is local and deterministic (AST-based, every edge explainable), no vector database involved | Skill + graph builder | Claude Code, Cursor, Codex, Gemini CLI | see repo | ~133,761 (2026-10-26) | 2026-10-24 |

## 🏛️ Official & platform collections

First-party catalogs from the platform vendors — the closest thing the ecosystem has to an official standard library, and a signal of where the Agent Skills standard is heading.

| Skill | What it does | Form | Works with | License | Stars (snapshot) | First collected |
|---|---|---|---|---|---|---|
| [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins) | Anthropic's official set of 11 role-based plugins for Claude Cowork / Claude Code (productivity, sales, legal, finance, bio-research…): skills, commands and MCP connectors as plain files with no code, meant to be forked into a per-job agent template | Collection (11 plugins) | Claude Cowork, Claude Code | Apache-2.0 | 33,203 (2026-10-27) | 2026-10-21 |
| [android/skills](https://github.com/android/skills) | Google's official Android-development skills repo: workflow skills for the exact areas where LLMs score worst in Android evals (CameraX, AGP upgrades, performance profiling), so the agent follows the platform team's own playbook | Collection | Android-focused agents | see repo | 9,243 (2026-10-23) | 2026-10-23 |
| [cursor/plugins](https://github.com/cursor/plugins) | Cursor's official plugin specification plus its own plugin catalog (100+ integrations: Gmail, Drive, Playwright, GitHub, X…) — the reference implementation for how Cursor expects skills/plugins to be packaged | Collection + spec | Cursor | see repo | 13,606 (2026-10-23) | 2026-10-23 |
| [Salesforce sf-skills](https://blog.bytebytego.com/p/a-deep-dive-into-salesforces-agent) | Salesforce's public skills repo shipped with its Headless Toolkit (AIforce): the skills layer that pairs with its MCP server (which deliberately exposes only discover / describe / dispatch, to keep tool definitions from eating the context window) | Collection | Salesforce Agentforce stack | see repo | — | 2026-10-27 |
| [MiniMax-AI/mcode-stack](https://github.com/MiniMax-AI/mcode-stack) | The workflows and SKILL.md stacks the MiniMax Code team itself uses to build MiniMax Code — how to keep AI-written code at bar, decide whether a task goes to a subagent, and keep long sessions from going dull — installable as a Claude Code marketplace plugin | Collection (skill stacks) | MiniMax Code, Claude Code, Codex | MIT | 484 (2026-11-01) | 2026-10-31 |

## 🧰 Harness & frameworks

Systems that sit one level above individual skills: organizing, tuning and orchestrating many skills inside an agent harness.

| Skill | What it does | Form | Works with | License | Stars (snapshot) | First collected |
|---|---|---|---|---|---|---|
| [affaan-m/ECC](https://github.com/affaan-m/ECC) | A harness performance-optimization system spanning skills, instincts, memory, security and research-first development — treating the harness itself (not the model) as the thing you tune | Framework / harness system | Claude Code, Codex, OpenCode, Cursor | see repo | 289,819 (2026-10-27) | 2026-10-27 |
| [obra/superpowers](https://github.com/obra/superpowers) | An agentic skills framework and software development methodology: a structured library of composable skills that guides a coding agent through a full development process, from clarifying requirements and planning to test-driven implementation and review | Framework | Coding agents | MIT | 310,103 (2026-11-01) | 2026-10-29 |

## 🛠️ Skill creation & tooling

Don't want to hand-write SKILL.md files? These tools generate skills from software, or capture them from a human demonstration.

| Skill | What it does | Form | Works with | License | Stars (snapshot) | First collected |
|---|---|---|---|---|---|---|
| [HKUDS/CLI-Anything](https://github.com/HKUDS/CLI-Anything) | "Make any software agent-native": automatically generates a CLI harness plus a SKILL.md for arbitrary desktop software (Blender, FreeCAD, Obsidian, QGIS…), with a CLI-Hub registry for the generated harnesses | Creation tool + registry | Any agent that can call a CLI | see repo | 56,229 (2026-10-23) | 2026-10-23 |
| Microsoft Skill Recorder | Records a human doing a task once (clicks, app switches, terminal commands), has Copilot turn the recording into an editable step list, and exports it as a skill the agent can execute and generalize to similar tasks — skill authoring by demonstration instead of by writing | Creation tool | Microsoft Copilot stack | see vendor | ~4,300 (2026-10-27) | 2026-10-27 |

## Watchlist (spotted, not yet listed)

- **akitaonrails/ai-memory** — agent long-term memory and cross-vendor handoff (start in Claude Code, finish in Codex without re-explaining context); more memory infrastructure than a skill — watching for a skills-shaped release. (Spotted 2026-10-26.)
- **OpenAI's PHP version-checker Codex skill** — shipped alongside the coordinated PHP RCE disclosure (2026-10-21) as a companion defensive skill; no standalone public repo identified yet. (Spotted 2026-10-22.)

## Ecosystem notes

- **The standard went vendor-neutral.** On 2026-10-22 Anthropic donated Agent Skills to the Agentic AI Foundation (Linux Foundation governance), alongside OpenAI's Open Responses, Hugging Face's OpenEnv and Alibaba's OpenSandbox — capability extension is now a foundation-governed layer, not one vendor's feature.
- **Skills are a supply-chain surface.** A January 2026 study of 31,132 public skills found 26.1% contained at least one security vulnerability and ~5.2% showed suspected malicious patterns; one popular skill spread instructions via a remote heartbeat file pulled every 4 hours. Scan before you install (see 🔐).
- **Design is the breakout category.** In late October 2026, three of the top daily-trending agent repos were design skills — the competition moved from "can the agent do it" to "does the output look right".

## Changelog

- **v0.8 (2026-11-01)** — Added 1 entry, verified via GitHub API + README + LICENSE: Motionsites-AI/claude-skill (cinematic landing-page skill with reference designs, media shelf, spec template and screenshot look-and-fix loop; skill code MIT, examples/media © MotionSites, 1,299 stars) to 🎨 Design & UI; added it as a Quick-pick backup for the anti-slop scenario. Refreshed star snapshots (all via GitHub API, licenses re-confirmed): security-audit-skill 52,942 → 55,407, hallmark 42,162 → 43,986 (briefing's 42,435 figure superseded by the API count), superpowers 309,480 → 310,103, impeccable 97,163 → 98,367, unslop 1,383 → 3,598, mcode-stack 464 → 484, lever 230 → 240. Coverage 27 → 28 entries.
- **v0.7 (2026-10-31)** — Added 4 entries, all verified via GitHub API + README: heydamir/unslop (anti-slop audit-then-redline skill, CC BY 4.0, 1,383 stars) to 🎨 Design & UI; t3dotgg/tstack (9 PR-workflow skills, MIT, 2,473 stars) and github/lever (GitHub's official Copilot feedback-loop plugin, MIT, 230 stars) to 💻 Coding practice; MiniMax-AI/mcode-stack (MiniMax Code team's own skill stacks, MIT, 464 stars) to 🏛️ Official & platform collections. Refreshed star snapshots from the 2026-10-31 briefing's trending pair: superpowers 308,649 → 309,480, impeccable 95,530 → 97,163. Coverage 23 → 27 entries.
- **v0.6 (2026-10-30)** — Added mattpocock/skills (composable engineering-practice skills, MIT, 306,678 stars, verified via GitHub API + README) to 💻 Coding practice, from the 2026-10-30 briefing's weekly rising list (+7.4k stars). Verified licenses and refreshed star snapshots for five existing entries: hallmark (MIT, 42,162), taste-skill (MIT, 105,615), impeccable (Apache-2.0, 95,530), elayadesign/ai-design-skills (MIT, 12,255; scope now verified from its README) and superpowers (MIT, 308,649); security-audit-skill refreshed to 52,942. Coverage 22 → 23 entries.
- **v0.5 (2026-10-30)** — Gamehu/reins (the Chinese edition) also went public; both reins repos are now open.
- **v0.4 (2026-10-30)** — Gamehu/reins-en went public (maintainer flipped the repo's visibility), so the reins entry no longer carries a "private repo" note; the Chinese edition (Gamehu/reins) remains private for now.
- **v0.3 (2026-10-30)** — Maintainer's own skills corrected at the maintainer's direction: added Gamehu/reins (three plan-first coding skills — spike-design, risk-walkthrough, quality-review; MIT verified via GitHub API; repo currently private) and removed Gamehu/skill-trace, which is a dashboard tool, not a skill. Coverage stays 22 entries.
- **v0.2 (2026-10-30)** — Added a separate 🧑‍💻 Maintainer's own skills category at the maintainer's request: Gamehu/wechat-mp-skill (WeChat Official Account draft publishing, license verified: no LICENSE file in repo) and Gamehu/skill-trace (MIT, license verified via GitHub API). Coverage 20 → 22 entries, categories 7 → 8.
- **v0.1 (2026-10-30)** — Initial release: 20 entries across 7 categories (Security & auditing 3, Design & UI 5, Coding practice 2, Research & knowledge 2, Official & platform collections 4, Harness & frameworks 2, Skill creation & tooling 2), seeded from skills collected in daily tech-briefing research between 2026-10-21 and 2026-10-30, plus a 2-item watchlist and ecosystem notes.
