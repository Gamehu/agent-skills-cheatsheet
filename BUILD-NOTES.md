# Build Notes — Agent Skills Cheatsheet (public repo)

## What this repo is

- Public repo: `Gamehu/agent-skills-cheatsheet` — a daily-maintained, classified catalog of agent skills (SKILL.md packages, plugin collections, frameworks, scanners, creation tools).
- Sibling of `Gamehu/open-model-cheatsheet`; same conventions: English, evidence-first, CC BY 4.0 document license, versioned header + changelog, dated snapshots instead of live claims.
- Local working copy: `~/workspace/goals/goal-2/files/agent-skills-cheatsheet-en/`
- Built 2026-10-30 at Hu's request ("新建一个 repo，用来维护你每天收集到的 skill……做好分类，每个 skill 的描述信息要明确").

## Entry standard (binding for the daily sync)

Every entry must have:

1. **Name + link** — the project's canonical repo (or official page if there is no repo).
2. **What it does** — ONE sentence, plain language: the problem + the mechanism. No marketing copy, no vague praise ("powerful", "revolutionary" are banned). If the mechanism is unknown, say what is known and mark the entry `unverified`.
3. **Form** — exactly one of: Single skill / Collection / Framework / Scanner / Directory / Creation tool (combinations allowed, e.g. "Skill + command set").
4. **Works with** — only agents/platforms the source actually states; otherwise "Coding agents" is not allowed as a guess — write what the source supports or leave the generic "agent skills standard" only when the source says so.
5. **License** — from the repo's LICENSE / GitHub license field (first-hand). "see repo" until verified; never guess.
6. **Stars (snapshot)** — cumulative stars with the date of the snapshot in parentheses. Never present a snapshot as a live count; refresh on re-verification.
7. **First collected** — the date the entry first entered this catalog.

## Categories (fixed taxonomy; propose changes to Hu before adding a new one)

0. 🧑‍💻 Maintainer's own skills — Gamehu's own skills and skill-ecosystem tooling ONLY (currently wechat-mp-skill and skill-trace). Nothing collected from third parties goes here, and the maintainer's projects do not get duplicated into the other categories.
1. 🔐 Security & auditing — auditing agent output; scanning/auditing skills themselves; benchmarked directories.
2. 🎨 Design & UI — design vocabularies, processes, anti-slop skills.
3. 💻 Coding practice — engineering style/methodology skills that change how code gets written.
4. 🔬 Research & knowledge — domain skill packs; knowledge-graph / knowledge-base skills.
5. 🏛️ Official & platform collections — first-party catalogs from platform vendors.
6. 🧰 Harness & frameworks — systems that organize/tune/orchestrate many skills.
7. 🛠️ Skill creation & tooling — generators and capture tools that produce new skills.

An item goes in exactly ONE category (its primary purpose); cross-references go in Quick picks, not duplicate rows.

## Daily sync rules

- Sources, in order: (a) that morning's daily IT briefing file (`~/workspace/goals/daily-it-news-briefing/briefs/YYYY-MM-DD-每日IT资讯简报.md`) — skills surface there first; (b) GitHub trending / search for new skill projects; (c) ecosystem press and community discussion.
- Verify every NEW entry against its GitHub repo (description, license, stars) via the API or repo page before listing; unverifiable entries go to the Watchlist section, not the tables.
- Update existing entries only on a verified change (new star snapshot, license confirmed, scope change); record the new snapshot date.
- Bump the version (v0.x, minor bump per day with changes), update the header line, README coverage count + "Last sync" date, and prepend a changelog entry — all in the same commit.
- Commit message: `Daily sync vX.Y: <one-line English summary>`; git identity `-c user.name=Gamehu -c user.email=gamehu@yeah.net`; push `origin main`.
- No-change days: no commit, report "no material change".
- Do NOT spawn further subagents from inside the sync run.
