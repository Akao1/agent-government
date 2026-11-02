# Agent Government · Governing AI Agents with the Chinese Imperial Bureaucracy

> Govern your AI agents with the ancient Chinese civil service system (Three Departments + Six Ministries + Grand Secretariat + Censorate) — a set of role contracts, functional routing, and memory institutions, battle-tested in a real multi-tool environment.

**[中文 README](./README.md)**

---

## Why a "Government" for Agents

If you maintain projects with multiple AI coding tools (Claude Code / Codex / ZCode / DSH...) over months, you've probably hit these five walls:

1. **Volatile context** — every session starts fresh; last week's judgments and lessons are gone
2. **Unreliable self-review** — the same model drafting and reviewing equals signing its own homework
3. **No coordination across tools** — three tools editing in parallel, overwriting each other, memories forking
4. **No routing for requests** — writing, coding, and research all crammed into one pipeline (or no pipeline at all)
5. **Scope creep by AI** — quietly editing global configs, auto-approving its own plans, making the calls that were yours to make

This repo's answer is not another agent framework, but a layer of **institution**: split "who drafts, who reviews, who executes, who audits, who decides" apart, then fix them in place with role contracts (files), official memory (archives), and functional routing (ministries). **The government is additive, not a framework** — it replaces none of your existing tools; it just issues them official seals.

## Core Principles

| Principle | One-liner | Institutional design |
|---|---|---|
| **Officials flow like water, clerks stand like rock** | Agents with judgment serve only for the duration of a task; judgment-free programs run persistently | Scheduler scripts ("clerks") run 24/7 with zero discretion; officials materialize on demand, retire when done, leave archives behind |
| **The drafter never approves** | AI may draft the proposal (piaoni); the choice always stays human (pihong) | The Grand Secretariat only produces paper; edicts touching global rules / irreversible ops / publishing / payment require human approval |
| **Three Departments are workflow, Six Ministries are functions** | The decision flow (draft → veto → execute) is orthogonal to functional partitions | Requests route to a ministry first, then run the pipeline |
| **Institutional memory crosses projects; case files never do** | An official's craft travels with the office; a project's secrets stay home | Official archives live globally; facts from project A are structurally unable to leak into project B |
| **The reviewer must not be the drafter** | Same-executor review must be labeled as such, never faked as independent | The same_tool principle: three blind-drafted ballots per deliberation, provenance honestly labeled |
| **Censors patrol, never garrison** | Auditing is periodic and mobile — never resident, never colluding, never a bottleneck | One censor patrols all six ministries by checklist: post-release spot check + weekly patrol + anomaly-triggered impeachment |

## The Full Chart

```
Emperor (You) —— Approval (major matters need your red ink; no proxy, no default, no auto-approve)
  │
Grand Secretariat (cross-project · 3 Secretaries · draft only, never execute)
  │  Outputs an "Edict": decision + routing + whether approval is required
  │  Three tiers: Memorandum / Deliberation / Countersign
  │  Ballots drafted mutually blind · dissent preserved verbatim
  │      ↑Edict veto: Chancellery (Shizhong)    ↑Ballot veto: Censorate
  ↓Edict (minor matters execute directly; major ones await approval)
Three Departments + Six Ministries (outside the Secretariat · the administration)
  Secretariat (zhongshu): turn edicts into "memorials" (task contracts/design/acceptance)
  Chancellery (menxia): veto edicts + subordinates review deliverables
  Department of State (shangshu): Puye = the current session model
    (Shangshu Ling = your scheduler script — permanently vacant)
    └─ Six Ministries (per-workspace functional partitions):
       Personnel / Revenue / Rites / War / Justice / Works
Censorate (cross-project · independent): patrol checklist · post-release spot checks
  · impeachment · archive audits · case closure review · ballot veto
```

**Mapping offices to tools** (key: programs never hold judgment):

| Office | Actual counterpart | Key constraint |
|---|---|---|
| Emperor | The user | Approval power is exclusive; no proxy |
| 3 Secretaries | Three independent drafting agents (or one agent, three perspectives) | Three prohibitions: never swallow dissent / never approve for the human / never execute while drafting |
| Zhongshu Ling | Requirements-analyst role | Drafts the "how"; never decides the routing |
| Shizhong | Independent-reviewer role | Vetoes edicts + reviews deliverables; never drafts |
| Shangshu Ling | Task scheduler script | **Permanently vacant** — the title goes to the program, the judgment stays with agents and the human |
| Puye | Current session model | Does the actual scheduling |
| Six Ministers | Lead contracts of each functional partition | Countersign power (review ballots from their domain); never join the Secretariat |
| Censor | Independent audit agent | Inspect only, never modify; never an executor of the same task |

## Quick Start

Three steps to adopt in your own multi-AI environment:

**Step 1: Define functional routing (Six Ministries)**

Copy [`docs/职能分区.md`](docs/职能分区.md) and adapt the table to your work types. Example mapping: Personnel=memory & rules, Revenue=knowledge retrieval, Rites=writing, War=development, Justice=testing & audit, Works=infrastructure. No need to fill all six — start with two or three.

**Step 2: Set up contracts and archives**

- Drop the contracts from [`templates/`](templates/) into your agents/ directory (most AI tools support "role files / subagent definitions")
- Create `records/` and initialize each official's archive from [`templates/records-template.md`](templates/records-template.md)
- Add one line to your tool's entry file (AGENTS.md / CLAUDE.md / system prompt): read the government charter first to route each task

**Step 3: Wire up mechanisms you already have**

The government builds no new execution machinery — map it onto your existing tools:

| Government function | You can use |
|---|---|
| Department-of-State scheduling | Any task pipeline script, TODO tooling |
| Locks / occupancy | Any file lock (prevent two sessions writing one file) |
| Patrol triggers | Cron jobs running audit scripts |
| Drafting & approval | Your tool's plan-approval mode / confirmation prompts |
| Official memory | Plain files + on-demand retrieval (see [`docs/官员记忆规范.md`](docs/官员记忆规范.md)) |

## FAQ

**Q: Why not resident agents?**
Residency means: ever-dirtier context (cross-project contamination), anchor fixation (one early bias pollutes every later task), single point of failure, zero auditability. "Officials flow" means every awakening is freshly bound by contract, with a clean context, naturally parallel. Duties needing 24/7 presence go to "clerks" (judgment-free programs).

**Q: I only have one AI tool. Does it still work?**
Yes. The Three Departments become three phases of the same model (analyze → blind cross-review → execute); the three-ballot deliberation becomes multiple independent generations by the same model (label provenance honestly).

**Q: Why Chinese imperial naming?**
Not nostalgia — because the Tang dynasty already thought these problems through: the Chancellery's veto = independent review; imperial examination & rotating officials = judgment flows, preventing entrenchment; itinerant censors = auditors isolated from the audited; the avoidance rule = case files never cross regions. A millennium of institutional trial-and-error, compressed.

**Q: Didn't the Three Departments eventually decline?**
Yes — and its causes are exactly this system's firewalls: too many layers → everything bypassed via "slanted envelopes" → institutions hollowed out. Hence the red lines here: small tasks must take the fast lane (memorandum / direct answer), censors must never become release bottlenecks, and every proposed new office must first answer "what real gap? what executable check?"

## License

[MIT](./LICENSE)
