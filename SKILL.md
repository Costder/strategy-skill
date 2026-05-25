---
name: strategy
description: Use when a user wants a long-running /strategy goal system, evidence-based planning, autonomous task execution, subagent delegation, goal rerouting, or a strategic advisor that keeps working until blocked by approvals or missing input.
version: 2.0.0
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [strategy, goals, planning, autonomous-execution, subagents, metrics, rerouting]
    related_skills: [writing-plans, subagent-driven-development, opentrust-agent-payments, opentrust-registry-network]
---

# Strategy Skill — Path to Victory

## Overview

`/strategy` is a long-term thinking skill for agents.

Use it when a goal is too big for a simple list.

Most agents can make tasks. That is easy. But a task list can still be wrong.

`/strategy` helps the agent slow down and ask better questions first:

- What does the user really want?
- Is this the best path?
- Do the numbers work?
- Does this fit the user’s time, money, skill, and risk?
- What should the agent do first?
- When should the agent stop or change the plan?

Then it builds a living route:

```text
True Outcome
→ Vehicle Selection
→ Goal Initialization
→ Assumptions + Exit Conditions
→ Paths
→ Milestones
→ Tasks
→ Subagent Jobs
→ Metrics
→ Feedback
→ Strategic Review / Reroute
```

Core promise: never build a confident plan for a goal that fails its own math.

## Why Users Benefit

Users get:

- a clearer goal
- a better path
- smaller next steps
- less wasted work
- safer agent action
- a way to know when the plan is failing
- a way to pivot before wasting months
- less busywork for the user

The skill helps the agent do more than ask, “What should I do?”

It makes the agent ask, “Should we do this this way?”

## `/strategy` vs `/goal`

`/goal` is for tracking a goal.

`/strategy` is for thinking through the best path to reach it.

| Command | Best for | What it does |
|---|---|---|
| `/goal` | A target you want to track | Saves the goal and checks progress |
| `/strategy` | A hard goal that needs a plan | Tests the goal, picks a path, makes tasks, checks reality, and reroutes |

Use `/goal` when the user already knows what they want and just needs tracking.

Use `/strategy` when the goal is big, risky, unclear, long-term, or expensive.

Example:

```text
/goal Lose 20 pounds
```

This tracks the target.

```text
/strategy Lose 20 pounds while working full time and staying under $100/month
```

This builds a plan that fits real life.

## Installation / Quick Start

Install this skill as `strategy` and use it when the user needs a long-term plan, not a one-off answer.

Example prompts:

```text
/strategy Get a remote software job in 6 months
/strategy Launch my app and reach 500 paying users
/strategy Lose 40 lb safely this year
/strategy Build a portfolio site and publish weekly
```

If the host has not wired a slash command yet, preload the skill and treat the user’s message as the `/strategy` goal input.

**Optional trust layer:** For paid tools, agent marketplaces, delegated workers, or spend-capable strategies, pair this skill with **OpenTrust**. OpenTrust adds signed tool/agent passports, spend policies, revocation, payment quotes, and deny-first verification so autonomous strategy work can safely discover, hire, and pay outside agents without trusting random endpoints by default.

## When to Use

Use this skill when the user wants:
- a `/strategy ...` command or strategy mode
- a long-term goal turned into an executable route
- autonomous private work with approval gates
- subagent delegation for each ready task
- metrics, assumptions, and exit conditions tracked over time
- a plan that adapts when reality disagrees with assumptions
- a sharp advisor that challenges the goal before planning

Do not use it for:
- a one-off answer
- a simple todo list
- public posting, emailing, spending, deploying, or account changes without explicit approval
- legal, medical, or financial commitments

## Command Boundary

`/strategy` is the public Path to Victory command.

Do **not** use `/goal` for this skill. `/goal` is a separate command/surface and must not be overloaded.

Private deployments may have aliases, but public docs and general users should see `/strategy`.

## Updated Execution Flow

```text
Goal Input
  ↓
LAYER 0: Strategic Reasoning
  → Query Learning Log for prior relevant findings
  → Clarify true underlying outcome
  → Identify viable vehicle types
  → Stress-test math on each vehicle
  → Run Environment Check
  → Score vehicles against Operator Constraint Profile
  → Select vehicle or flag mismatch
  → Produce Vehicle Selection Record
  ↓
LAYER 1: Goal Initialization
  → Ask 5 setup questions
  → Register Assumption Registry (min 3 assumptions required)
  → Set Exit Conditions
  → Define success metrics
  ↓
LAYER 2: Path / Milestone / Task Generation
  → Generate paths scoped to selected vehicle
  → Generate milestones
  → Generate executable tasks with full schema
  ↓
LAYER 3: Scoring + Dispatch
  → Score tasks by priority formula
  → Run Load Balancer check before dispatching
  → Dispatch safe tasks within bandwidth limit
  → Gate on approvals for public/irreversible actions
  ↓
LOOP
  1. Load goals, paths, tasks, metrics, approvals, budgets, active jobs
  2. Recover stale or interrupted jobs
  3. Update metrics
  4. Run Signal Intake Layer and check assumptions against actuals
  5. If assumption broke, trigger Strategic Review protocol
  6. Check Exit Conditions
  7. Check operator load score
  8. Find ready tasks
  9. Score tasks
  10. Run Load Balancer check
  11. Dispatch safe tasks
  12. Log outputs and update Learning Log when milestones/goals complete
  13. Ask only for blockers
  14. Reroute if path is failing
```

## Layer 0 — Strategic Reasoning

Layer 0 runs once per new goal before the normal 5 setup questions. It should feel like a sharp advisor having a 10-minute conversation, not an interrogation.

Sequence:

1. **Clarify the true underlying outcome**
   - Look past the stated goal.
   - Example: “launch app” may really mean “financial independence by 35.”
   - Ask: “What does success actually look like in your life?”

2. **Identify viable vehicle types**
   - Business: SaaS, services, marketplace, high-ticket, physical product.
   - Employment: job, consulting, freelance.
   - Investment: equity, real estate, assets.
   - Hybrid combinations.
   - Do not assume the stated path is the best path.

3. **Stress-test the math on each viable vehicle**
   - What revenue/profit numbers are required?
   - What margins, volume, and price points does that imply?
   - What is the realistic timeline?
   - What capital, skills, or connections are prerequisites?

4. **Run Environment Check**
   - Is the space crowded?
   - Who are the main players?
   - Is timing favorable, neutral, or unfavorable?
   - Are there tailwinds, headwinds, dependencies, or timing constraints?

5. **Score each vehicle against the Operator Constraint Profile**
   - Available capital.
   - Available hours per week.
   - Current skill set, honestly measured.
   - Current network/distribution.
   - Risk tolerance.
   - Hard blockers.

6. **Select the best-fit vehicle or flag mismatch**
   - If achievable, proceed with the chosen vehicle.
   - If unrealistic, say so clearly before building any path.
   - Never build a plan for a goal that fails its own math.

### Vehicle Selection Record

Store one Vehicle Selection Record per goal:

```json
{
  "true_outcome": "string",
  "vehicles_considered": [
    {
      "vehicle": "string",
      "implied_revenue": "string",
      "implied_customers_or_clients": "string",
      "implied_timeline": "string",
      "prerequisite_capital": "string",
      "prerequisite_skills": ["string"],
      "operator_fit_score": "high | medium | low | mismatch",
      "verdict": "recommended | viable | hard | mismatch"
    }
  ],
  "environment_assessment": {
    "market_crowding": "low | medium | high",
    "timing": "favorable | neutral | unfavorable",
    "key_risks": ["string"],
    "key_tailwinds": ["string"],
    "overall_environment_score": "green | yellow | red"
  },
  "selected_vehicle": "string",
  "selection_rationale": "string",
  "goal_is_realistic": true,
  "flags": ["string"]
}
```

If `overall_environment_score` is `red`, do not block automatically, but require operator acknowledgment before moving into Layer 1.

## Operator Constraint Profile

Build this once during Layer 0. Reference it in every planning, scoring, and dispatch decision.

```json
{
  "operator_id": "string",
  "available_capital": 0,
  "available_hours_per_week": 0,
  "current_skills": ["string"],
  "current_network": "description string",
  "risk_tolerance": "low | medium | high",
  "hard_constraints": ["string"],
  "active_goals": ["goal_id"],
  "current_load_score": 0
}
```

Rules:
- No path or task may require capital greater than `available_capital` unless explicitly staged as “requires future funding.”
- No week’s task load may exceed `available_hours_per_week`.
- Update the profile whenever the operator reports a change.
- Recalculate `current_load_score` every loop cycle.
- If there are 3+ active goals for a solo operator, warn every loop cycle.

## Layer 1 — Goal Initialization

Run the original 5 setup questions only after Layer 0 completes:

```text
1. What outcome do you want?
2. By when?
3. How will we measure success?
4. What should I never do without asking?
5. What tools/accounts/files can I use?
```

If the user already gave enough detail, do not ask again. State assumptions and continue.

Each goal stores:

```json
{
  "goal_id": "G1",
  "title": "Launch my app and reach 500 paying users",
  "deadline": "2026-12-31",
  "mode": "builder",
  "selected_vehicle": "string",
  "metrics": {
    "users": {"current": 0, "target": 500, "source": "manual"},
    "paid_users": {"current": 0, "target": 50, "source": "api"}
  },
  "paths": ["P1"],
  "approval_policy": "standard",
  "status": "active"
}
```

## Assumption Registry

Every path and milestone is built on assumptions. Make those assumptions visible.

```json
{
  "assumption_id": "string",
  "goal_id": "string",
  "path_id": "string",
  "statement": "string",
  "type": "conversion | cac | timeline | demand | pricing | skill | other",
  "assumed_value": "string",
  "actual_value": null,
  "status": "unvalidated | confirmed | broken | updated",
  "last_checked": "ISO date string",
  "impact_if_broken": "low | medium | high | critical"
}
```

Rules:
- Every new path must register at least 3 assumptions before tasks are generated.
- Check assumptions during each loop cycle when relevant metrics exist.
- If an assumption changes to `broken`, trigger Strategic Review.
- Surface assumptions with `/strategy assumptions [goal_id]`.
- Existing goals without assumptions should be prompted for backfill on the next loop cycle, but should not be blocked.

## Exit Conditions

Every goal needs predefined kill and pivot triggers. Dead strategies should not run forever.

```json
{
  "exit_conditions": {
    "kill_triggers": [
      {
        "metric": "string",
        "condition": "string",
        "threshold": "string",
        "evaluation_window_days": 0
      }
    ],
    "pivot_triggers": [
      {
        "metric": "string",
        "condition": "string",
        "threshold": "string",
        "evaluation_window_days": 0
      }
    ],
    "max_budget": 0,
    "max_timeline_days": 0,
    "paths_exhausted_action": "kill | pivot | escalate_to_operator"
  }
}
```

Defaults if the operator does not specify:
- Kill trigger: core metric has not moved after 90 days of active execution.
- Pivot trigger: core metric is under 30% of target after 50% of timeline elapsed.
- Budget kill: total cost exceeds max budget.
- Path exhaustion: if P1 and P2 both fail, escalate before generating P3.

Rules:
- Evaluate exit conditions every loop cycle.
- When a kill trigger fires, pause all tasks, notify the operator, and summarize what was learned.
- When a pivot trigger fires, rerun Layer 0 with updated data.
- Never silently kill a goal.

## Layer 2 — Paths, Milestones, Tasks

Only generate paths after Layer 0 selects a viable vehicle.

Every task must be executable by a subagent. Avoid vague tasks like “do marketing.” Prefer tasks with clear deliverables.

Task schema stays compatible with v1:

```json
{
  "task_id": "G1-P1-T3",
  "title": "Draft 10 outreach messages for target users",
  "department": "growth",
  "status": "ready",
  "autonomy_level": 1,
  "depends_on": ["G1-P1-T1"],
  "deliverable": "Markdown file with 10 drafts",
  "success_metric": "ready_to_approve_outreach",
  "estimated_cost": 0.05,
  "estimated_hours": 1.5,
  "priority": 7.2
}
```

Task states remain:

| State | Meaning |
|---|---|
| `backlog` | Known but not ready |
| `ready` | Can be dispatched now |
| `deferred` | Waiting for time, dependency, or bandwidth |
| `dispatched` | Subagent is working |
| `blocked` | Needs approval, credential, input, or manual user action |
| `done` | Deliverable complete and logged |
| `failed` | Recovery failed; needs review |
| `cancelled` | Intentionally stopped |

## Layer 3 — Scoring, Bandwidth, Dispatch

Keep the v1 priority formula:

```text
priority = value + urgency + confidence + synergy - effort - cost - risk
```

Before dispatching any task, run Load Balancer check:

```text
1. Calculate current weekly hour load across all active goals.
2. If projected load > operator available_hours_per_week:
   → Do not dispatch.
   → Mark task as deferred with reason: bandwidth.
   → Suggest lower-priority tasks to pause or drop.
3. If load_score > 80%, show yellow flag.
4. If load_score > 100%, show red flag and stop dispatching.
```

Load score:

```text
sum(estimated_hours for all dispatched + ready tasks this week)
÷ available_hours_per_week
× 100
```

Recommended solo-operator limit: 2 active goals at a time.

## Subagent Dispatch

Every ready task is sent to a subagent with a clear contract.

```text
You are working on Strategy task [TASK_ID].

Goal: [goal title]
Selected vehicle: [vehicle]
Task: [task title]
Mode: [simple/builder/engineer/coach]
Autonomy level: [0-4]

Context:
- Current metric state: [metrics]
- Operator constraints: [capital, hours, skills, network, risk]
- Assumptions this task depends on: [list]
- Dependencies completed: [list]
- Relevant files/URLs: [list]
- User constraints: [approval policy, budget, tone]

Load relevant skills if available.

Deliverable:
- Produce [specific artifact]
- Save it at [path] if file output is expected
- Do not perform Level 3+ actions
- If blocked, return the exact approval/input needed

Final response must include:
- status: done / blocked / failed
- files created or changed
- metric changes, if any
- assumptions affected, if any
- next recommended task
```

## Autonomy and Approval Gates

| Level | Name | Strategy may do this without asking |
|---|---|---|
| 0 | Private thinking | Read local notes, summarize, plan, score, organize private state |
| 1 | Private execution | Write drafts, create files, run tests, edit private project files, do web research |
| 2 | Reversible external prep | Prepare submissions, stage posts, draft emails, open local PR branches, prepare deploy plans |
| 3 | Approval required | Post publicly, email/DM people, spend money, push code, deploy, change accounts, submit forms |
| 4 | Never autonomous | Legal/medical/financial commitments, impersonation, unsafe actions, sharing private info without approval |

Rule: if a user would reasonably feel surprised it happened, ask first.

## Signal Intake Layer

Run after metrics update in every loop cycle.

Default deviation thresholds:

| Metric Type | Review Trigger |
|---|---|
| `conversion_rate` | 50% deviation |
| `cac` | 100% deviation |
| `timeline` | 25% slip |
| `revenue` | 30% below projection |

Rules:
- For each active goal, compare actual metrics to assumptions.
- If actual deviates beyond threshold, flag assumption as `broken`.
- Calculate impact score.
- If impact is `medium` or higher, queue Strategic Review.
- If impact is `critical`, pause the path and notify the operator immediately.

## Strategic Review Protocol

Strategic Review is not ordinary task rerouting.

When an assumption breaks:

```text
1. Identify which assumption broke.
2. Re-run Layer 0 vehicle stress-test with updated real numbers.
3. Evaluate whether the current path is still viable.
4. If yes, adjust milestones and task estimates.
5. If no, generate alternative path options and present them to the operator.
6. Never silently continue a path that has failed its assumptions.
```

## Learning Log

Strategy should get smarter across goals.

```json
{
  "learning_id": "string",
  "source_goal_id": "string",
  "category": "assumption | vehicle | task_type | market | operator_behavior",
  "finding": "string",
  "confidence": "low | medium | high",
  "applicable_contexts": ["string"],
  "date_logged": "ISO date string"
}
```

Rules:
- At goal completion or kill, run a retrospective and log at least 3 findings.
- At every new Layer 0 run, query the Learning Log by vehicle type, market, and operator profile.
- Surface relevant prior learnings before committing to a new path.
- Start empty. Do not pre-populate it with fake wisdom.

## Metrics

Every goal needs at least one success metric.

Metric sources:
- `manual` — user updates it
- `file` — Strategy reads a local file
- `api` — Strategy calls an endpoint
- `derived` — calculated from other metrics
- `subagent` — reported by completed work

If metrics are stale, Strategy says so. If most metrics are stale, it avoids major reroutes and asks for updated data.

## Communication Rhythm

Keep communication low-noise.

| Cycle | Purpose | Message? |
|---|---|---|
| Morning | recover jobs, update metrics, dispatch work, ask one important question | Yes, short |
| Midday | continue work if budget and gates allow | No, unless blocked |
| Evening | summarize completed work, cost, blockers, next steps | Yes, short |
| Night | quiet private work only | No, unless urgent |
| Weekly | review evidence, reroute, prune goals, plan next week | Yes |

## Observability Commands

Public command names:

| Command | Output |
|---|---|
| `/strategy status` | all active goals and running tasks |
| `/strategy status path=<name>` | filtered path view |
| `/strategy status goal=<goal_id>` | one goal |
| `/strategy status task=<task_id>` | one task |
| `/strategy watch <task_id>` | live progress updates |
| `/strategy blocked` | approvals and manual actions needed |
| `/strategy costs` | budget and spend |
| `/strategy metrics` | metric state and staleness |
| `/strategy assumptions [goal_id]` | assumption registry |
| `/strategy vehicles [goal_id]` | vehicle selection record |
| `/strategy load` | operator bandwidth/load score |
| `/strategy learnings` | cross-goal learning log |
| `/strategy exits [goal_id]` | kill/pivot conditions |

Progress should be real or coarse. If a subagent cannot report real progress, show elapsed time instead of fake percentages.

## Storage Shape

Default local state:

```text
~/.hermes/strategy/
  goals.json
  operator_profile.json
  vehicle_selection_records.json
  assumptions.json
  exit_conditions.json
  tasks.json
  metrics.json
  approvals.json
  dispatch_log.json
  cost_tracker.json
  recovery_log.json
  learning_log.json
  work/
```

Existing deployments may use another backend. Keep adapters backward compatible.

## Backward Compatibility

Do not break existing active goals.

If an existing goal has no Vehicle Selection Record, Assumption Registry, Operator Constraint Profile, or Exit Conditions:
- mark it `needs_strategy_v2_backfill`
- prompt the operator on the next loop cycle
- keep safe work running if it does not violate approval or bandwidth rules
- do not silently invent missing constraints

## Common Mistakes

| Mistake | Fix |
|---|---|
| Taking the stated goal at face value | Run Layer 0 and clarify the true outcome first |
| Building a plan that fails its math | Stress-test vehicle economics before paths |
| Ignoring operator constraints | Check capital, hours, skills, network, risk, hard blockers |
| Creating invisible assumptions | Register at least 3 assumptions per path |
| Treating broken assumptions as task failures | Trigger Strategic Review, not just reroute tasks |
| Overloading a solo operator | Run Load Balancer before every dispatch |
| Letting dead strategies run forever | Evaluate Exit Conditions every loop |
| Learning nothing across goals | Write retrospective findings to Learning Log |
| Posting or spending too early | Draft and stage first, ask before external action |
| Confusing `/strategy` with `/goal` | Keep command boundaries separate |

## Acceptance Checklist

The v2 implementation is complete when:

- [ ] Layer 0 runs before any path is generated on a new goal
- [ ] Vehicle Selection Record is produced and stored per goal
- [ ] Operator Constraint Profile is built at first run and persisted
- [ ] Every new path registers at least 3 assumptions before tasks
- [ ] Signal Intake Layer runs every loop cycle and flags broken assumptions
- [ ] Strategic Review triggers when impact is medium or higher
- [ ] Load Balancer check runs before every dispatch
- [ ] Exit Conditions are required at goal initialization, with defaults if missing
- [ ] Learning Log is written to at goal completion or kill
- [ ] Learning Log is consulted at every new Layer 0 run
- [ ] Existing active goals remain backward compatible

## Success Criteria

Strategy is working when:
- the user can start a long-term strategy in one command
- the engine challenges the goal before planning
- the chosen vehicle fits the operator’s real constraints
- assumptions are visible and checked against reality
- tasks stay within bandwidth
- subagents complete safe private work
- approval requests are rare, clear, and previewed
- metrics improve or Strategy recommends a real pivot/kill/reroute
- costs stay within budget
- the system survives downtime without losing trust
