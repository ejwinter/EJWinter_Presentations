---
title: "Beyond the Prompt"
info: |
  Teaching Your AI to Think Like Your Team and Level Up with Skills
  Eric Winter — 2026-04-17
---

# Beyond the Prompt

Teaching Your AI to Think Like Your Team<br>and Level Up with Skills

**Eric Winter** · Research Genomics · 2026-04-17

<!--
Welcome. Tonight we are going from "how do I write better prompts?" to something much deeper:
how do you build an AI engineering culture that compounds over time as individuals, teams,
and the organization contribute to a shared knowledge base.
-->

---

# Agenda

- The limits of prompt engineering
- Spec-Driven Development (recap)
- Constitutions — teaching your AI your standards
- Memory — context that learns and grows
- Rules — breaking the constitution into focused pieces
- Skills — reusable AI capabilities you can build and share
- Commands — automating workflows, not just guiding them
- Bringing it all together

<!--
A roadmap of the session so attendees know where we're headed and can follow the
thread across demos. Each section builds on the last — we end with a decision
framework that makes clear which tool to reach for and why.
-->

---

# How Most Developers Use AI Today

<div class="grid grid-cols-2 gap-8 mt-4">
<div>

**The familiar pattern**

- "How do I write a regex for emails?"
- "Explain this error message"
- Inline autocomplete for the current line
- Tab to accept, keep typing

</div>
<div>

**What it feels like**

- A very fast Google with context
- A rubber duck that writes code
- A pair programmer who stays in their lane

</div>
</div>

> The model helps — but *you* are still writing the software.

<!--
Show of hands: how many have used Copilot or ChatGPT this way? Most developers
are still in Q&A mode — asking questions, getting answers, copy-pasting.
Even GitHub Copilot's inline completion is really just "finish my sentence."
The AI is a tool you operate, not a collaborator that acts.
-->

---

# The Paradigm Shift: Agents That *Do* the Work

<div class="grid grid-cols-2 gap-8 mt-4">
<div>

**Old model (assistant)**
- You write code, AI autocompletes
- You ask questions, AI answers
- You drive, AI is a GPS

</div>
<div>

**New model (agent)**
- You describe intent, AI implements
- Agent reads your codebase, runs tests, iterates
- You review, AI does the labor

</div>
</div>

**Claude Code, Copilot Workspace, Devin, Cursor Composer**

These agents open files, run terminal commands, edit code across the whole repo, and loop until the tests pass — without you touching a keyboard.

---

# But who's keeping it on track?

<div class="grid grid-cols-2 gap-6 mt-2">
<div>

**Iterative refinement**
- Review the diff, redirect the agent
- "That's wrong — do it this way instead"
- Works, but requires you to catch every mistake

</div>
<div>

**Context guardrails** ← *this talk*
- Teach the agent your standards upfront
- It applies them without being asked
- Scales across your team, not just you
- Speeds up iterations

</div>
</div>

> Iterative refinement keeps *one task* on track. Context guardrails keep *every task* on track.

<!--
This is the key tension to name early. Anyone who's used an agent has done iterative
refinement — you review, you correct, you steer. It works, but it's exhausting at scale.
The rest of this talk is about context guardrails: constitutions, memory, rules, skills,
and commands. These are the mechanisms that shift the agent from "capable but unpredictable"
to "consistent and trustworthy." You're still in control — but you're not babysitting.
-->

---
layout: section
---

# The Limits of<br>Prompt Engineering

---

# The Problem with Simple Prompts

- Large-context tools (Claude Code, Copilot) give the agent your entire codebase
- More context ≠ better results — without focus, the model can't prioritize
- "Add a login page" leaves scope, constraints, and standards entirely up to the model
- Result: hallucinated APIs, ignored conventions, features that drift from intent

<!--
Tools like Claude Code give the agent a massive context window — your entire codebase,
terminal history, open files. But more context without focus means the model makes
confident guesses about intent, stack choices, and behavior.
-->

---

# Hallucination Gets Worse at Scale

- Larger context = more surface area for the model to go off-track
- Without anchors, the model guesses — confidently and plausibly
- Mistakes compound: one wrong assumption early leads to a cascade

<!--
The larger the context, the more surface area for the model to go off-track.
Without anchors, the model makes confident guesses about intent, stack choices,
and behavior. Mistakes compound — a wrong assumption early leads to a cascade
of plausible-but-wrong code.
-->

---

# The Fix: Structured Focus

Three complementary layers that narrow the solution space:

- **Spec** — defines *what* to build and the acceptance criteria
- **Constitution** (AGENTS.md / CLAUDE.md) — defines *how* to build it
- **Skills** — enumerate *specific capabilities* the agent should apply

Together these shift the model's attention from guessing your intent to executing it.

<!--
You can't prompt your way out of this. You need to constrain the problem space
before the prompt. Specs keep the agent on task. A constitution means you never
re-explain your stack. Skills apply institutional knowledge consistently.
-->

---
layout: section
---

# Spec-Driven Development

---

# Ground the AI in Specs Before Writing Code

- Maintain living documents: functional specs, acceptance criteria, prioritized backlog
- AI reads these as context — knows *what* to build, *why*, and what's out of scope
- Eliminates scope creep and hallucinated features
- Spec is consumed and completed; constitutions and skills persist indefinitely

<!--
Spec-Driven Development means the agent starts every task with a clear, bounded
understanding of what done looks like. The spec scopes the task, defines acceptance
criteria, and tells the agent exactly what done means.
-->

---

# Backlog.md — Specs in Your AI Tool

- Tasks created from specs before implementation begins
- Agent queries the backlog at session start for context and constraints
- Agent marks tasks done and updates spec docs as work completes
- Backlog lives in the repo — whole team shares the same picture

<!--
Backlog.md is an MCP server that brings spec-driven development into your AI tool.
Documentation stays accurate because the AI maintains it, not just generates code.
This is a recap of prior work — tonight we go deeper into what happens around the specs.
-->

---
layout: section
---

# Constitutions

Teaching Your AI Your Standards

---

# What a Constitution Is

- A structured Markdown file read by the agent at the start of every session
- The single source of truth for how work gets done on this project
- Not a prompt — a persistent, version-controlled contract between the team and the AI
- If it isn't accurate enough for a new engineer to follow, it isn't accurate enough for the agent

<!--
AGENTS.md, CLAUDE.md, COPILOT-INSTRUCTIONS.md — different names, same idea.
A well-written constitution is valuable even if no one on the team uses AI.
New engineers can onboard faster by reading it. Treat it as a first-class artifact:
reviewed in PRs, updated when the stack changes, owned by the team.
-->

---

# What Goes In a Constitution

- **Project structure** — directory layout, what belongs where, non-obvious conventions
- **Stack** — canonical libraries for every concern; versions where they matter; off-limits libs
- **Standards** — style guides, linting rules, naming conventions, architectural rules
- **Workflow** — how PRs work, how tests run, what done looks like

<!--
Especially important for less common languages or frameworks where training data is
thinner (e.g. NgRx, Pydantic v2, SQLAlchemy async) — the model needs explicit guidance,
not inference. The agent will default to whatever it saw most in training; your stack
list overrides that default.
-->

---

# Personal → Team → Organizational

- Start personal: encode your own preferences and workflow
- Extend to the team: shared standards, stack decisions, naming conventions
- Grow to the org: cross-team invariants, security requirements, compliance rules
- Constitutions must be living documents — stale constitutions mislead

<!--
A static constitution quickly becomes ineffective. Living constitutions are reviewed
in PRs, updated when the stack changes, and owned by the team — not just the person
who wrote the first draft.
-->

---
layout: center
---

# Demo: Constitution in Action

```bash
# Explore the TeamFabric root constitution
cat TeamFabric/CLAUDE.md

# Explore the template team constitution
cat TeamFabric/Fabric/template/CLAUDE.md

# Explore the core behavioral rules
cat TeamFabric/Fabric/template/fabric-core.md
```

> Prompt: *"Add a new team member named Alex Chen who joins the platform engineering team as a senior engineer at 100% allocation."*

<!--
Show: role separation in CLAUDE.md (framework dev instructions vs team constitution template).
Show: @import composition in Fabric/template/CLAUDE.md.
Show: meta mode, entity structure, and context log rules in fabric-core.md.
Live: run the member add prompt against the Example/ instance.
-->

---

# TeamFabric: Layered Constitution

Framework rules are imported. Team rules live below the line — updates never overwrite them.

```md
@.claude/fabric-core.md
@.claude/fabric-triage.md
@.claude/fabric-product.md
@.claude/fabric-standup.md
@.claude/fabric-retro.md

# {{TEAM_NAME}}

<!--
  Everything below this line is yours.
  TeamFabric updates will not touch this section.

  TO CUSTOMIZE BEHAVIOR:
    - Override or extend rules here, below the @imports
    - Add team-specific commands to .claude/commands/
    - Add team-specific skills to .claude/skills/
-->
```

<!--
The @import lines are framework-owned. Everything below the comment is team-owned.
When /update-fabric runs, it rewrites the imported files but never touches the team section.
This is how you get framework updates without losing your customizations.
-->

---

# TeamFabric: Core Rules

One focused file. One concern: how entities work, what meta mode is, who can edit what.

```md
## Meta Mode

Structural files are read-only during normal operations.
Edits require meta mode.

Entering meta mode:
- User explicitly invokes `/meta`
- AI may suggest it when a structural change is implied

## Entity File Structure

1. **Lightweight header** — cheap to load, identifies relevance quickly
2. **First-class structured fields** — curated, human-guided artifacts
3. **Context log** — append-only breadcrumb trail

### Context Log Entry Format
- YYYY-MM-DD HH:MM - Who (contact) via channel: Summary.
  Source: [reference to original artifact]
```

<!--
This is what a focused rule file looks like. One file, one concern.
The meta mode rules protect structural integrity. The entity structure rules
define a token-efficient layering: cheap headers for scanning, rich context logs
for depth. The agent knows exactly how to read and write these without being told
every session.
-->

---
layout: section
---

# Memory

Context That Learns and Grows

---

# What Memory Is

- Structured Markdown files the agent writes and reads across sessions
- Captures what the agent has learned: preferences, decisions, feedback, external pointers
- Lives in `.claude/memory/` — loaded selectively, not dumped wholesale
- Unlike a constitution, you don't author memory directly — the agent maintains it

> "You seem to be correcting me a lot on that I am going to remember this."

<!--
Constitutions are written by humans and encode what you know in advance.
Memory is different — it's context the agent accumulates by working with you,
persisting what it learns so you don't have to repeat yourself across sessions.
-->

---

# The Four Types of Memory

| Type | What it captures | Example |
|------|-----------------|---------|
| `user` | Who you are, how you work | "Senior Go engineer, new to React" |
| `feedback` | Corrections that should stick | "Never mock the database in tests" |
| `project` | Decisions, motivations, not in git | "Auth rewrite is compliance-driven" |
| `reference` | Pointers to external systems | "Bugs in Linear project INGEST" |

<!--
User memories tailor future behavior to your profile. Feedback memories prevent
the agent from making the same mistake twice. Project memories capture the why
behind decisions — things git history doesn't know. Reference memories tell the
agent where to look in external systems.
-->

---

# Constitution vs. Memory

| | Constitution | Memory |
|--|-------------|--------|
| **Authored by** | Human team | Agent |
| **Reviewed via** | PRs | Your oversight |
| **Answers** | How do we always work? | What has this agent learned? |
| **Signal you need it** | Re-explaining setup every session | Correcting the same thing across sessions |

<!--
A constitution is what you deliberately encode as permanent team standards.
Memory is what the agent learns organically by working with you.
The practical effect: a constitution keeps the agent consistent;
memory keeps the agent from making the same mistake twice.
-->

---

# TeamFabric: Breadcrumb Memory

No raw content retained. Every interaction leaves a structured, sourced breadcrumb.

```md
## Entity File Structure

Each entity uses a layered information architecture:

1. **Lightweight header** — cheap to load, identifies relevance
2. **First-class fields** — curated artifacts maintained through refinement
3. **Context log** — append-only breadcrumb trail of sourced summaries

### Context Log Entry Format

- YYYY-MM-DD HH:MM - Who (contact) via channel: Summary with reasoning.
  Source: [reference to original artifact]
```

<!--
This is memory at the entity level — not a session-level memory file, but the same
principle. The agent never rewrites history. It appends breadcrumbs with timestamps,
sources, and reasoning. The summary may become stale (flagged) but the log is
append-only. You always know what was said, by whom, via what channel, and why.
-->

---
layout: section
---

# Rules

Breaking the Constitution Into Focused Pieces

---

# What a Rule Is

- A focused Markdown file that encodes one specific concern
- Lives in `.claude/rules/` — discovered and loaded automatically
- Each rule has a **scope** that controls when it is loaded
- The constitution becomes an index; rules become the chapters

A monolithic CLAUDE.md loads everything, every time — most of it irrelevant.<br>
Rules keep the active context lean.

<!--
As a project grows, a single CLAUDE.md becomes long, hard to maintain, and loads
context the agent doesn't always need. Rules decompose the constitution into modular,
scoped instruction files — loaded precisely when they're relevant.
-->

---

# The Four Rule Scopes

| Scope | When it loads | Best for |
|-------|--------------|---------|
| **Always** | Every session | Core conventions, non-negotiables |
| **Auto-attached** | File matching glob is in context | Language-specific, framework patterns |
| **Agent-requested** | Agent reads description and pulls | Deep reference, optional style guides |
| **Manual** | User explicitly references it | One-off tasks, migration guides |

<!--
Always rules fire on every session — keep these small and truly universal.
Auto-attached rules are the most powerful: the Python style guide loads when
editing .py files, the API contract rules load when editing routes/ — nothing else.
-->

---

# How the Agent Decides What to Load

The agent never sees full rule/skill content upfront — it reads **descriptions first**, then pulls the full file only if relevant.

<div class="grid grid-cols-2 gap-6 mt-4">
<div>

**What loads eagerly (cheap)**
- Rule/skill name
- One-line `description` field
- Glob pattern (for auto-attached rules)

</div>
<div>

**What loads on demand (expensive)**
- Full rule body
- Full skill instructions
- Examples and constraints

</div>
</div>

**The description is the decision gate.**<br>Write it as a trigger condition, not a label.

| Instead of... | Write... |
|---|---|
| `"Python style guide"` | `"Use when editing any .py file or reviewing Python PRs"` |
| `"TDD skill"` | `"Use when implementing any feature or bugfix, before writing implementation code"` |

<!--
This is the mental model that unlocks effective rule and skill authoring.
The agent does a two-pass load: metadata first (always cheap), full content only when
the description suggests it's relevant. A vague description like "Python style guide"
gives the agent nothing to match against — it has to guess. A trigger condition
("use when editing .py files") is unambiguous. Same pattern applies to agent-requested
rules and skills equally — the description IS the routing logic.
-->

---

# Rules vs. Skills

| | Rules | Skills |
|--|-------|--------|
| **Role** | Extend and modularize the constitution | Define capabilities invoked on demand |
| **When active** | Always in the background | Called in when needed |
| **Best for** | Standards and constraints | Specific task playbooks |

Rules are your team's standing orders.<br>
Skills are the specialist playbooks you hand out for specific missions.

<!--
This distinction matters. A rule says "always align equals signs in Terraform."
A skill says "here is how to write a Terraform module end to end."
Rules constrain; skills enable.
-->

---

# TeamFabric: Module System as Rules

Each module is a scoped rule file. Teams opt in at init time — only relevant rules load.

```md
@.claude/fabric-core.md       ← always loaded (core rules)
@.claude/fabric-triage.md     ← loaded when Triage enabled
@.claude/fabric-product.md    ← loaded when Product enabled
@.claude/fabric-standup.md    ← loaded when Standup enabled
@.claude/fabric-retro.md      ← loaded when Retro enabled

## Enabled Modules

| Module   | Status   | Notes                                    |
|----------|----------|------------------------------------------|
| Core     | Enabled  | Team definition, members, ingestion      |
| Triage   | Enabled  | Request intake, rubric evaluation        |
| Product  | Enabled  | Product definitions and context          |
| Backlog  | Disabled | Epic/feature/work-item hierarchy         |
| Standup  | Disabled | Daily standup conversations              |
```

<!--
Each @import is a rule file with a clear single responsibility.
Teams that don't use standups don't load the standup rules.
The context stays lean — the agent only knows about what's actually in use.
-->

---

# TeamFabric: A Rule File

One file. One module. Everything the agent needs to know about request triage — nothing else.

```md
# TeamFabric Module: Triage

## Overview
The Triage module manages request intake, evaluation workflows,
and rubric-based assessment. Teams customize the specific rubrics
and workflow definitions in `requests/workflow/`.

## Behavioral Rules

- New requests are created in `requests/<request-id>/request.md`
  using the workflow's request template.
- Request IDs follow the pattern `R-NNN` (sequential, zero-padded).
- When evaluating, always load the full rubric from the workflow
  definition. Do not evaluate from memory.
- After evaluation, surface the recommendation clearly but do not
  make the accept/reject decision — that belongs to the decision-maker.
```

<!--
Single responsibility. Triage rules don't know about backlog, standup, or retros.
The agent loads this file when triage work is happening and nothing else.
The behavioral rules are imperative and specific — not guidelines, not suggestions.
-->

---
layout: section
---

# Skills

Reusable AI Capabilities You Can Build and Share

---

# What a Skill Is

- A packaged prompt — a structured Markdown file defining a specific, reusable capability
- Tells the agent *exactly* how to approach a task: steps, constraints, what good output looks like
- Skills are composable — build a library, invoke only what's relevant
- Named procedures your agent can call, not instructions you re-explain every session

<!--
Think of them as named procedures your agent can call, rather than instructions
you re-explain every session. They're invoked on demand, keeping the baseline
context lean until expertise is actually needed.
-->

---

# How Skills Get Invoked

A skill's `description` frontmatter is what the agent reads to decide whether to load it.

```markdown
---
name: test-driven-development
description: Use when implementing any feature or bugfix,
             before writing implementation code
---

## Steps
1. Write a failing test first...
```

The agent sees the `description` only — the full skill body stays out of context until invoked.

**You control selectivity through the description:**
- Broad trigger → loads often, keeps agent behavior consistent across many tasks
- Narrow trigger → loads rarely, reserves specialized guidance for specific moments
- No trigger → agent guesses — avoid this

<!--
The description field is doing double duty: it's documentation for humans AND
routing logic for the agent. The more precise your trigger condition, the more
reliably the agent knows when this skill applies. This is why skill authors
write things like "TRIGGER when: code imports anthropic" rather than just
"Claude API skill." Explicit beats implicit every time.
-->

Skills are distributed through GitHub and discoverable at **skills.sh**

<!--
Without skills, the model infers the right approach from training data — which means
it defaults to whatever was most common in its training set, not what your team
actually wants.
-->

---

# Installing Skills

```bash
# No global install required
node --version   # 18+

# Install a single skill
npx skills add https://github.com/hashicorp/agent-skills \
  --skill terraform-style-guide

# Install all skills from a repo
npx skills add https://github.com/hashicorp/agent-skills

# See what's installed
npx skills list
```

Skills are stored in `.claude/skills/` and committed to the repo — the whole team shares them.

<!--
The skills CLI syncs skill repos into your project. Once committed, every teammate
gets the same agent behavior. No prompt sharing, no wiki pages — the skill is the source.
-->

---

# What Makes a Great Skill

- **Single responsibility** — one skill, one domain
- **Opinionated, not optional** — makes decisions: "use `for_each` over `count`"
- **Concrete over abstract** — show examples, name libraries, give exact patterns
- **Tells the agent what NOT to do** — constraints are as valuable as instructions
- **Written for the agent, not a human** — imperative, direct, no hedging
- **Tested** — invoke it, see what the agent does, refine until reliable

<!--
The description field is the most important line in the skill — get it wrong and the
skill never fires. Include specific phrases users naturally say. Avoid overlap with
other skills — ambiguous triggers produce unpredictable behavior.
-->

---
layout: center
---

# Demo: Skills in Action

```bash
# See TeamFabric's installed skills
ls TeamFabric/Fabric/.claude/skills/

# Read the ingestion skill
cat TeamFabric/Fabric/.claude/skills/ingestion.md
```

> Drop a raw meeting note into `TeamFabric/Example/staging/` and run:
>
> `/ingest staging`

<!--
Show the ingestion skill file — trigger conditions, three paths, context log format.
Then drop a real meeting note into staging/ and run /ingest staging.
Watch the agent classify, summarize, propose a context log entry, and wait for confirmation.
No code. Pure markdown instructions producing structured output.
-->

---

# TeamFabric: A Skill File

Clear purpose. Explicit trigger conditions. Step-by-step procedure. No ambiguity.

```md
# Skill: Content Ingestion

## Purpose
Process incoming content into Fabric's structured entity model.
The core "people dump raw content in, AI organizes it" capability.

## Three Ingestion Paths

### Quick File
User provides content plus an entity hint.
Trigger: "this is for R-42" or "file this under WI-1234"
Procedure:
1. Load the referenced entity's header and recent context log.
2. Summarize the content against that entity's context.
3. Present the proposed context log entry for confirmation.
4. On confirmation, append to the entity's context log.
5. Set the entity's staleness flag if summary may affect first-class fields.
```

<!--
Notice the structure: purpose in one sentence, trigger condition stated explicitly,
procedure as a numbered list with no ambiguity. The agent can't misread this.
Compare this to a comment in a README — the skill is the specification, not the docs.
-->

---

# TeamFabric: Skills vs. Rules

A rule constrains. A skill enables.

| | Rule (`fabric-triage.md`) | Skill (`ingestion.md`) |
|--|--------------------------|----------------------|
| **Loaded** | When triage module enabled | When ingestion task detected |
| **Says** | "Always load rubric from file" | "Here are the three ingestion paths" |
| **Role** | Constrains agent behavior | Gives agent a procedure to execute |
| **Scope** | Applies to all triage work | Invoked for this specific capability |

<!--
The triage rule tells the agent what it must and must not do in triage context.
The ingestion skill tells the agent HOW to execute ingestion when the moment arrives.
You need both: rules for standing orders, skills for specialist playbooks.
-->

---
layout: section
---

# Commands

Automating Workflows, Not Just Guiding Them

---

# What a Command Is

- A Markdown file in `.claude/commands/` that becomes a `/slash-command`
- When invoked, its contents are injected directly into the conversation as a prompt
- Unlike skills, commands can include **executable bash blocks** that run before Claude processes the request
- Think of them as scripts with an AI attached: first automate, then reason

<!--
Commands automate a specific, recurring workflow. They're the most powerful tool
in this set because they can execute real code before the AI ever sees the result —
giving the agent real, live context rather than static instructions.
-->

---

# Skills vs. Commands

| | Skills | Commands |
|--|--------|---------|
| **Purpose** | Teach the agent a capability | Automate a repeatable workflow |
| **Trigger** | Agent detects relevance | User invokes with `/` |
| **Execution** | Pure prompt | Can run bash before AI engages |
| **Best for** | Coding standards, patterns | Ops tasks, doc generation, scaffolding |

Skills make the agent smarter about *how* to do something.<br>
Commands make the agent faster at *doing* something specific, every time.

<!--
A well-designed command eliminates the "how do I even start this?" friction for
recurring team tasks. The bash execution is the key differentiator — you can gather
real runtime state (git diff, file listings, test output) and hand it to the AI
already parsed and ready for reasoning.
-->

---
layout: center
---

# Demo: Commands in Action

```bash
# Read the status command
cat TeamFabric/Fabric/.claude/commands/status.md

# Run status against the example instance
# (open Example/ in Claude Code, then)
/status

# Generate a mindmap report
/report mindmap
```

<!--
Show the status command file — pure AI instructions, no bash, but very structured output spec.
Then run /status live. Then /report mindmap to show what a generated HTML report looks like.
The report command does have bash-equivalent steps — it reads the backlog tree and builds HTML.
-->

---

# TeamFabric: A Command File

Instructions written directly to the AI. The agent reads this file and follows it exactly.

```md
# /status - Team Status Summary

## Purpose
Quick factual snapshot of current team state.
Numbers and lists, not narrative.

## Behavior

1. Load:
   - team/team.md (members, allocation, current state)
   - Active member profiles (capacity adjustments for current/upcoming periods)
   - Request counts if available

2. Output a concise summary:

Team: [name]
Effective Capacity: [X] FTE

Active Members:
  [name] - [role] - [allocation]%

## Notes
- Read-only, no meta mode required.
- Keep it short. If the user wants narrative, point them to /describe-team.
```

<!--
No code. The command IS the specification. The agent reads it, loads the right files,
formats the output exactly as specified. The output format is in the command file itself
so it's consistent every time any engineer on the team runs /status.
-->

---
layout: section
---

# Case Study: A Product Engineering Team

Carrying the Toolkit Across Projects

---

# The Portable Toolkit

<div class="grid grid-cols-3 gap-6 mt-4">
<div>

**Constitution**
- Project-specific stack
- Directory conventions
- PR and test workflow
- Compliance requirements

*Adapts per project*

</div>
<div>

**Skills**
- `frontend-design`
- `angular-architecture`
- `database-design`

*Authored once, installed everywhere*

</div>
<div>

**Rules**
- `functional-spec-codevelopment`
- `manualtesting-codevelopment`

*Auto-attached by file glob — no per-session setup*

</div>
</div>

> The constitution adapts. The skills and rules travel unchanged.

<!--
This is the practical payoff of the whole talk. A team that has invested in skills
and rules carries their institutional knowledge from project to project without
re-explaining it. The constitution is the only thing that changes — the agent's
capabilities and standing orders are already loaded on day one.
-->

---

# The Project Constitution

One file the agent reads at session start. Every engineer gets the same agent behavior.

```md
# CLAUDE.md — Inventory Manager

## Stack
- Frontend: Angular 18 + NgRx + Angular Material
- Backend: .NET 8 Web API + EF Core  
- DB: PostgreSQL 16 · Auth: Entra ID (MSAL)

## Standards
- Components: smart/dumb pattern; no logic in templates
- State: NgRx feature stores only — no component-local state for shared data
- API: RESTful; use ProblemDetails for all error responses
- Schema changes via EF Core migrations only — no manual SQL

## Workflow
- Branch from `main`; PRs require passing CI and one review
- Skills installed: frontend-design, angular-architecture, database-design
- Rules installed: functional-spec-codevelopment, manualtesting-codevelopment
```

<!--
The constitution is project-specific but short. It names the stack so the agent
never defaults to whatever it saw most in training. It names the installed skills
and rules so the agent knows what to expect. A new engineer can read this and
know exactly how the team works — that's the bar.
-->

---

# Skills: Expertise On Demand

<div class="grid grid-cols-3 gap-4 mt-2">
<div>

**`frontend-design`**

*Trigger: building any UI component, page, or layout*

- Produces accessible, production-quality interfaces
- Enforces component composition patterns
- Applies Angular Material conventions
- Flags UX anti-patterns before code is written

</div>
<div>

**`angular-architecture`**

*Trigger: creating or modifying Angular modules, components, services, or state*

- Enforces smart/dumb component split
- Scaffolds NgRx feature stores
- Applies service layer patterns
- Flags module boundary violations

</div>
<div>

**`database-design`**

*Trigger: designing schemas, writing migrations, or modeling data*

- Normalization decisions with rationale
- Index recommendations
- Migration safety checks
- EF Core conventions and override patterns

</div>
</div>

<!--
These three skills were authored once and committed to the team's shared skills repo.
Any engineer who installs the skills gets them on day one. The agent doesn't need to be told
how to do Angular or database design every session — and more importantly,
it applies *your team's* approach, not the internet's average approach.
-->

---

# Rules: Standards That Load Themselves

| Rule | Scope | What it enforces |
|------|-------|-----------------|
| **`functional-spec-codevelopment`** | Auto-attached: `docs/functional/**` | A living folder of docs describing *what the system does and why*, co-located with code — the agent keeps them synchronized as the code changes |
| **`manualtesting-codevelopment`** | Auto-attached: `tests/manual/**`, `*.testplan.md` | Co-authors test plans in parallel with implementation: steps, edge cases, regression checks |

```md
# Rule: Functional Spec Co-development
scope: auto-attach
globs: ["docs/functional/**"]

## Purpose
`docs/functional/` is the living record of what this system does and why.
It is co-authored by the agent and kept synchronized with the code at all times.

## Behavior
- When editing code, check whether a corresponding functional doc exists.
- If yes: update it to reflect the change. If no: create a stub and prompt the
  engineer to fill in the "why" before the PR is merged.
- Functional docs describe behavior and rationale — not implementation details.
  Those belong in code comments. These belong here.
```

<!--
The key insight: this isn't about specs written before coding starts. It's a living
folder that describes what the system does and why — maintained alongside the code
rather than abandoned after the first sprint. The rule makes the agent a co-author
of that documentation automatically. Engineers don't have to remember to update it.
-->

---

# The Pattern: Adapt the Constitution, Carry the Toolkit

<div class="grid grid-cols-2 gap-8 mt-4">
<div>

**Stays with the project**

Write once at kickoff, update as the project evolves.

- Stack and library choices
- Directory conventions
- PR and deployment workflow
- Security and compliance rules

</div>
<div>

**Travels with the team**

Install in minutes. Committed to a shared repo.

- `frontend-design`
- `angular-architecture`
- `database-design`
- `functional-spec-codevelopment`
- `manualtesting-codevelopment`

</div>
</div>

```bash
# New project setup
npx skills add https://github.com/your-org/agent-skills
# Write CLAUDE.md for this project — the agent is ready.
```

<!--
This is the compounding effect. The first project is expensive — you're writing skills
and rules from scratch. By the third project, you're spending twenty minutes on a
constitution and running one command. The agent arrives knowing your team's standards.
The institutional knowledge is in files, not in people's heads.
-->

---
layout: section
---

# Managing Context

---

# Context Is Not Free

Every token in the context window costs money — and attention.

<div class="grid grid-cols-2 gap-6 mt-4">
<div>

**Cost**
- Most providers charge per input token
- A full session with large files costs real money
- Long contexts make the agent slower to respond
- Accumulated noise degrades output quality

</div>
<div>

**Attention**
- Models weight recent tokens more than old ones
- A stale error from 20 messages ago still influences output
- Mid-task corrections get buried under conversation history
- A dirty context is a distracted agent

</div>
</div>

> The cleanest agent is one that starts fresh with exactly the context it needs.

<!--
Context management isn't just a cost optimization — it's a quality optimization.
A session that's been running for two hours has accumulated tool outputs, error messages,
half-completed thoughts, and corrections. The model treats all of that as signal.
Starting fresh — with guardrails instead of conversation history — produces more
consistent results than babysitting a long session.
-->

---

# Controlling Your Context

<div class="grid grid-cols-3 gap-4 mt-4">
<div>

**Clear it**<br>
`/clear`

Wipe the conversation. Your guardrails (constitution, rules, skills) reload automatically — you don't lose your standards, only the noise.

Best for: starting a new task in the same session.

</div>
<div>

**Compact it**<br>
`/compact`

Summarize the conversation into a compressed context block. Keeps continuity, reduces token count.

Best for: long-running tasks where you need to preserve state but are burning through tokens.

</div>
<div>

**Shelf it**<br>`/rename` then `claude --continue`

Give the session a meaningful name. Later, `claude --continue [name]` resumes it exactly where you left off.

Best for: "I'll come back to this" — a branch you're not done with yet.

</div>
</div>

**Quick escape:** `Ctrl+Z` suspends Claude, drops you to a plain shell. Run whatever you need. `fg` brings Claude back with the session intact.

<!--
Three tools, three different situations. /clear is the most important habit to build —
use it between tasks, not just when you're out of context. /compact is your pressure
valve for deep dives you can't abandon. /rename + --continue is your bookmarking system:
name the session for the branch or task, and you can pick it up tomorrow without
losing where you were. Ctrl+Z/fg is the one most people discover by accident —
worth calling out explicitly because it's genuinely useful for running a quick git
command or checking a file without opening a second terminal.
-->

---

# The Context Hygiene Habit

```
Finish a task  →  /clear  →  Start next task
```

**What survives a `/clear`**
- Your constitution (CLAUDE.md)
- Your rules (`.claude/rules/`)
- Your skills (`.claude/skills/`)
- Your memory (`.claude/memory/`)

**What gets wiped**
- Conversation history
- Tool output accumulation
- Mid-session corrections
- The model's "current mood"

> Your guardrails are durable. The conversation is disposable.

<!--
This is the practical takeaway. Everything you've built — constitutions, rules, skills,
memory — survives a /clear. That's the point of encoding standards in files rather than
in conversation history. When you /clear, you're not losing anything except the noise.
The agent reloads your guardrails fresh and starts the next task without baggage from
the last one.
-->

---
layout: section
---

# Bringing It All Together

---

# When to Reach for Each Tool

| Tool | Answers | Signal you need it |
|------|---------|-------------------|
| **Spec** | What to build right now | Agent keeps building the wrong thing |
| **Constitution** | How we always work | Re-explaining setup every session |
| **Memory** | What has this agent learned | Correcting the same mistake repeatedly |
| **Rule** | What applies in this context | CLAUDE.md only matters for some files |
| **Skill** | How to do this type of task | Writing the same multi-paragraph prompt |
| **Command** | Run this specific workflow | Shell script + explaining output every time |

These tools compound. Together they shift the team from *prompt engineering* to *engineering the agent*.

<!--
The clearest way to see the distinction: a spec answers "what are we doing right now?"
A constitution answers "how do we always work?" A rule answers "what applies here?"
A skill answers "how do we do this kind of thing?" A command answers "run this workflow."
None of them are substitutes for each other.
-->

---
layout: center
---

# Q&A

**Eric Winter**<br>
Research Genomics

<!--
Thank you. Happy to go deeper on any of these tools, talk about adoption strategies,
or look at specific examples from your own projects.
-->
