# Claude PM Plugin

> A practical Product Manager agent & command toolkit for **Claude Code / Claude CLI**

`claude-pm-plugin` is an **open-source, production-oriented Product Manager (PM) plugin** for Claude Code.

It provides:
- Structured **PM agents** (Discovery, PRD, Review, Priority, PM↔Tech bridge)
- Ready-to-use **CLI commands** (`/prd`, `/discover`, `/roadmap`, etc.)
- A workflow that bridges **product thinking → engineering execution**

This plugin is designed for **technical PMs, indie hackers, startups, and engineering-led teams**.

---

## ✨ Key Features

- 🧠 **Real PM thinking**, not generic prompts
- 🧩 **Engineering-friendly PRDs** (edge cases, acceptance criteria, risks)
- 🪓 **Anti–bullshit discovery** (challenge fake or premature requirements)
- 🔄 **Composable agents** (use one or chain many)
- ⚡ **Claude Code native** (no extra runtime, no SDK)

---

## 📦 Plugin Structure

```
claude-pm-plugin/
├── manifest.json
├── README.md
│
├── agents/
│   ├── pm_discovery.agent.md      # Requirement discovery & validation
│   ├── pm_prd.agent.md            # PRD generation (engineering-oriented)
│   ├── pm_review.agent.md         # Ruthless PRD / solution review
│   ├── pm_priority.agent.md       # Priority & roadmap planning
│   └── pm_tech_bridge.agent.md    # PM ↔ Engineering translation
│
└── commands/
    ├── discover.md                # /discover
    ├── prd.md                     # /prd
    ├── review-prd.md              # /review-prd
    ├── roadmap.md                 # /roadmap
    └── backlog.md                 # /backlog
```

---

## 🚀 Installation

### Option 1: Install from GitHub

```bash
plugin add https://github.com/yourname/claude-pm-plugin
```

### Option 2: Install locally

```bash
plugin add /absolute/path/to/claude-pm-plugin
```

Once installed, all commands will be available in Claude Code.

---

## 🧭 Available Commands

### `/discover` — Product Discovery
Use this when requirements are vague, rushed, or suspicious.

**What it does**:
- Separates *problem* from *solution*
- Identifies hidden assumptions
- Forces clarification before design

---

### `/prd` — PRD Generator
Generates an **engineering-ready PRD**, not a slide deck.

Includes:
- Scope / out-of-scope
- Normal & edge flows
- Data & metrics
- Acceptance criteria

---

### `/review-prd` — Ruthless Review
Reviews PRDs or solutions **from a tech lead’s perspective**.

Finds:
- Ambiguities
- Missing edge cases
- High-risk assumptions

---

### `/roadmap` — Priority & Roadmap Planning
Helps you make **hard trade-offs**.

Supports:
- RICE / MoSCoW-style prioritization
- MVP definition
- Explicit "not doing" decisions

---

### `/backlog` — Backlog Decomposition
Turns PRDs into:
- Epics
- Stories
- Tasks

Optimized for direct use in Jira / Linear / GitHub Issues.

---

## 🧠 Agents Overview

### 🧠 Product Discovery Agent
**Goal**: Prevent building the wrong thing.

Use when:
- A stakeholder gives a one-liner requirement
- The solution is proposed before the problem

---

### 🧩 PRD Writer Agent
**Goal**: Translate clarity into execution.

Optimized for:
- Engineers
- AI products
- B2B / internal tools

---

### 🧪 Ruthless Reviewer Agent
**Goal**: Break things early.

Acts like:
- A senior tech lead
- A grumpy architect

---

### 📊 Priority Planner Agent
**Goal**: Decide what *not* to build.

Useful when:
- Resources are tight
- Everything feels important

---

### 🔁 PM ↔ Tech Bridge Agent
**Goal**: Reduce PM–Engineering friction.

Outputs:
- Business-friendly explanation
- Engineering-friendly constraints
- Explicit trade-offs

---

## 🔄 Recommended Workflow

```
/discover
   ↓
/prd
   ↓
/review-prd
   ↓
/roadmap
   ↓
/backlog
   ↓
Engineering / Testing / Delivery
```

This mirrors how **strong PM + tech teams actually work**.

---

## 🎯 Who Is This For?

- Technical Product Managers
- Indie hackers / solo founders
- Engineering-led startups
- AI tool builders
- Teams tired of vague PRDs

---

## 🛠 Customization

You are encouraged to:
- Fork this repo
- Modify agent tone or strictness
- Add domain-specific agents (AI, EdTech, SaaS, infra)

This plugin is intentionally **plain-text + markdown** for easy hacking.

---

## 📌 Philosophy

> A good PM plugin should help you:
> - Ask harder questions
> - Write less bullshit
> - Ship fewer but better things

This plugin is opinionated by design.

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

## 🤝 Contributing

PRs are welcome for:
- New agents
- Better review checklists
- Industry-specific workflows

If you use this in production, consider sharing your setup.

---

## ⭐ Acknowledgements

Inspired by:
- Real-world PM & engineering collaboration
- Claude Code agent workflows
- Open-source AI tooling communities

---

Happy building.

