# Agent Skills Cheatsheet

> Version v0.4 · Data as of 2026-10-30 · Covers 22 entries · Daily-updated guide to agent skills for Claude Code, Codex, Cursor, OpenCode, Gemini CLI and other coding agents

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
| Your agent's UI looks like generic AI slop | Nutlope/hallmark | Purpose-built anti-slop design skill for the major coding agents | pbakaus/impeccable (design vocabulary + deterministic checks), Leonxlnx/taste-skill |
| Make the agent write less, better code | DietrichGebert/ponytail | "Lazy senior engineer" style skill with measured code/time reductions | multica-ai/andrej-karpathy-skills (Karpathy's practices as one CLAUDE.md) |
| Scientific research with an agent | K-Dense-AI/scientific-agent-skills | 177 ready-made research skills + 100+ scientific databases | Graphify-Labs/graphify (turn your codebase into a queryable graph first) |
| Give non-coding roles their own agent setup | anthropics/knowledge-work-plugins | Anthropic's official role-based plugin templates (sales, legal, finance…) | cursor/plugins (Cursor's official catalog) |
| Turn a desktop app into something an agent can drive | HKUDS/CLI-Anything | Auto-generates a CLI harness + SKILL.md for arbitrary software | Microsoft Skill Recorder (capture a human doing it once) |
| Organize / tune many skills at once | affaan-m/ECC | Harness performance system spanning skills, memory, security | obra/superpowers (agent skills framework) |

## 🧑‍💻 Maintainer's own skills

Skills written by this cheatsheet's maintainer, Gamehu — listed separately from the collected entries below, and held to the same entry standard.

| Skill | What it does | Form | Works with | License | Stars (snapshot) | First collected |
|---|---|---|---|---|---|---|
| [Gamehu/wechat-mp-skill](https://github.com/Gamehu/wechat-mp-skill) | A WeChat Official Account publishing skill: converts Markdown into WeChat-compatible HTML and creates/manages articles in the account's draft box through the WeChat API, with the token-cache and dynamic-IP whitelist failure modes (errors 40164 / 40001) documented from daily production use — it formats the maintainer's three daily briefings for WeChat | Single skill | SKILL.md-based agents | No LICENSE file in repo | 0 (2026-10-30) | 2026-10-30 (in production use since 2026-09-28) |
| [Gamehu/reins](https://github.com/Gamehu/reins-en) | Three skills that keep a coding agent on the plan you approved: `spike-design` turns a requirement into a reviewable, code-free plan — goals and non-goals, a structure skeleton, and an abstraction/dependency budget that defaults to zero — cut into ~300-line slices with numbered decisions; `risk-walkthrough` then walks only the hard parts of each slice and labels every deviation "needs your decision" or "already in the plan"; `quality-review` re-checks plan vs code in a fresh context and reports without ever editing. No runtime, nothing to install. (English edition linked; a Chinese edition lives at Gamehu/reins, still private.) | Collection (3 skills) | Claude Code, Codex, OpenCode | MIT | 0 (2026-10-30) | 2026-10-30 |

## 🔐 Security & auditing

Skills that audit agent output, and tooling that audits the skills themselves — the supply-chain layer of the skills ecosystem.

| Skill | What it does | Form | Works with | License | Stars (snapshot) | First collected |
|---|---|---|---|---|---|---|
| [cloudflare/security-audit-skill](https://github.com/cloudflare/security-audit-skill) | Turns a coding agent into a security auditor that works in six stages (recon → coverage-guided hunting → adversarial verification → structured output → independent re-check → neutral report), with finder and verifier kept separate so findings arrive with a full source trace instead of false-positive noise; Cloudflare runs it continuously over its own repos | Single skill | Coding agents (Claude Code class) | MIT | 48,529 (2026-10-27) | 2026-10-21 |
| [NVIDIA/SkillSpector](https://github.com/NVIDIA/SkillSpector) | Scans an agent skill *before you install it* for vulnerabilities, malicious patterns, prompt injection, data exfiltration and supply-chain risk — the pre-flight check for third-party SKILL.md files | Scanner | Claude Code, Codex, MCP skills | see repo | 22,164 (2026-10-27) | 2026-10-27 |
| [SkillzBench](https://signalnewsharrisonburg.com/press-releases/80473/skillzbench-launches-free-directory-that-security-scans-and-benchmarks-ai-agent-skills-before-agents-use-them/) | A free directory that security-scans every listed skill, benchmarks it with an A/B test (same model, with vs. without the skill, publishing the score delta — including negative ones), and serves your hand-picked set to your agent through an MCP connector | Directory + benchmark | Any agent via MCP | n/a (service) | n/a | 2026-10-26 |

## 🎨 Design & UI

Design skills exist because agent-generated interfaces converged on one generic "AI look". These give the agent a design vocabulary, a process, or explicit anti-slop rules.

| Skill | What it does | Form | Works with | License | Stars (snapshot) | First collected |
|---|---|---|---|---|---|---|
| [Nutlope/hallmark](https://github.com/Nutlope/hallmark) | An anti-"AI-slop" design skill: explicit rules and references that push a coding agent's front-end output away from the default gradient-and-glass look toward deliberate, product-specific design | Single skill | Claude Code, Cursor, Codex | see repo | 36,254 (2026-10-27) | 2026-10-25 |
| [pbakaus/impeccable](https://github.com/pbakaus/impeccable) | Gives a coding agent a shared design language: one `/impeccable init` writes the product facts into PRODUCT.md, 24 shared commands cover shaping, critique, polish and motion, and 61 deterministic checks run in the CLI or a browser extension without calling a model | Skill + command set | Coding agents (harness-level) | see repo | 89,159 (2026-10-27) | 2026-10-27 |
| [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) | A ten-stage design-taste workflow for agents, gated by real-browser verification tests, so "looks right" is checked in an actual browser instead of asserted by the model | Single skill (workflow) | Coding agents | see repo | ~104,000 (2026-10-30) | 2026-10-30 |
| [alchaincyf/huashu-design](https://github.com/alchaincyf/huashu-design) | An HTML-native design skill that returns deliverable design work from one prompt inside the agent — web/app prototypes, editable PPTX decks, animation and infographics — instead of a static mockup image | Single skill | Coding agents | see repo | 26,723 (2026-10-27) | 2026-10-27 |
| [elayadesign/ai-design-skills](https://github.com/elayadesign/ai-design-skills) | A design-skills pack for agents (surfaced on GitHub's daily trending chart); exact scope unverified — listed so the daily sync can verify and expand it | Collection | Coding agents | see repo | unverified | 2026-10-29 |

## 💻 Coding practice

Skills that change *how* the agent writes code — engineering judgment, house style and methodology, packaged as instructions the agent loads every run.

| Skill | What it does | Form | Works with | License | Stars (snapshot) | First collected |
|---|---|---|---|---|---|---|
| [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) | A "lazy senior engineer" persona skill that makes the agent write less code and verify more: measured on 39 tasks at −53% code volume, −41% time, with tests on 98% of high-risk logic; v5.3 adds a live cost/time/token band on top of Claude Code plus a local task board | Single skill | Claude Code | see repo | 169,603 (2026-10-21) | 2026-10-21 |
| [multica-ai/andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills) | Distills Andrej Karpathy's public observations on LLM coding pitfalls into a single CLAUDE.md skill file, so the agent inherits a well-known engineer's working rules without you writing them | Single skill (CLAUDE.md) | Claude Code | see repo | +3,286 in one week (2026-10-28) | 2026-10-26 |

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

## 🧰 Harness & frameworks

Systems that sit one level above individual skills: organizing, tuning and orchestrating many skills inside an agent harness.

| Skill | What it does | Form | Works with | License | Stars (snapshot) | First collected |
|---|---|---|---|---|---|---|
| [affaan-m/ECC](https://github.com/affaan-m/ECC) | A harness performance-optimization system spanning skills, instincts, memory, security and research-first development — treating the harness itself (not the model) as the thing you tune | Framework / harness system | Claude Code, Codex, OpenCode, Cursor | see repo | 289,819 (2026-10-27) | 2026-10-27 |
| [obra/superpowers](https://github.com/obra/superpowers) | An agent skills framework: a structured library of composable skills plus the methodology for invoking them, surfaced repeatedly on GitHub trending through October 2026; exact current scope to be re-verified by the daily sync | Framework | Coding agents | see repo | unverified | 2026-10-29 |

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

- **v0.4 (2026-10-30)** — Gamehu/reins-en went public (maintainer flipped the repo's visibility), so the reins entry no longer carries a "private repo" note; the Chinese edition (Gamehu/reins) remains private for now.
- **v0.3 (2026-10-30)** — Maintainer's own skills corrected at the maintainer's direction: added Gamehu/reins (three plan-first coding skills — spike-design, risk-walkthrough, quality-review; MIT verified via GitHub API; repo currently private) and removed Gamehu/skill-trace, which is a dashboard tool, not a skill. Coverage stays 22 entries.
- **v0.2 (2026-10-30)** — Added a separate 🧑‍💻 Maintainer's own skills category at the maintainer's request: Gamehu/wechat-mp-skill (WeChat Official Account draft publishing, license verified: no LICENSE file in repo) and Gamehu/skill-trace (MIT, license verified via GitHub API). Coverage 20 → 22 entries, categories 7 → 8.
- **v0.1 (2026-10-30)** — Initial release: 20 entries across 7 categories (Security & auditing 3, Design & UI 5, Coding practice 2, Research & knowledge 2, Official & platform collections 4, Harness & frameworks 2, Skill creation & tooling 2), seeded from skills collected in daily tech-briefing research between 2026-10-21 and 2026-10-30, plus a 2-item watchlist and ecosystem notes.
