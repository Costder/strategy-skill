---
name: strategy
description: Use when a user wants a long-running /strategy goal system, evidence-based planning, autonomous task execution, subagent delegation, goal rerouting, or a strategic advisor that keeps working until blocked by approvals or missing input.
version: 3.0.0
author: Costder
license: MIT
metadata:
  tags: [strategy, goals, planning, autonomous-execution, subagents, metrics, rerouting]
  related_skills: [writing-plans, subagent-driven-development]
---

# Strategy Skill — Path to Victory

## Runtime Adapter

`{strategy_store}` is a placeholder. Map it to whatever persistent storage your runtime supports.

Requirements:
- Atomic per-file read/write
- Key-value lookup by `goal_id`
- Survives process restart

Examples:
```
Hermes:      ~/.hermes/strategy/
Claude Code: .claude/strategy/
Generic:     ./strategy/ relative to working directory
Testing:     in-memory dict
```

All file references in this skill use `{strategy_store}/` as the prefix.

For strategies involving payments, external agent hiring, or spend authorization, pair with a trust/spend policy skill appropriate to your runtime.

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

`/goal` is a Ralph loop.

That means the user gives the agent one clear target, and the agent keeps working across turns until a judge says the target is done, blocked, paused, or out of budget.

`/goal` is powerful when the job is already clear.

`/strategy` is for the step before that.

It decides which target is worth giving to `/goal`, why that target matters, how to test it, and when to change course.

| Command | Best for | What it does |
|---|---|---|
| `/goal` | One clear job with a clear stop rule | Keeps the agent working across turns until done or blocked |
| `/strategy` | A big or risky outcome where the right path is not obvious | Picks the path, writes assumptions, sets stop rules, and creates clear work packets |

Simple rule:

```text
/goal = keep going until this job is done
/strategy = decide which job is worth doing, why, and when to change course
```

Another way:

```text
/goal is the engine.
/strategy is the steering wheel, map, dashboard, and brake.
```

Use `/goal` when the user knows the exact job and how to verify it.

Use `/strategy` when the goal is big, risky, unclear, long-term, or expensive.

A good split:

```text
/strategy Help me grow my app to 1,000 paying users.
```

Then Strategy may create a `/goal` packet like:

```text
/goal Build and test the first landing page experiment. Success means the page is live, analytics work, signup works, and the test plan is written.
```

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

Do not overload `/goal` to mean Strategy. `/goal` is its own Ralph-loop command.

But Strategy may produce clean `/goal` packets when the next step is clear enough for an execution loop.

Private deployments may have aliases, but public docs and general users should see `/strategy`.

## Updated Execution Flow

```text
Goal Input
  ↓
LAYER 0: Complexity Gate → 0-A Discovery (stable gate) → 0-B Stress-Test (realistic gate)
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
  4. Run Signal Intake Layer — PCE-score each active assumption
  5. If PCE score < 0.1, pause path and notify operator
  6. If PCE score 0.1–0.3, flag for Strategic Review on next cycle
  7. Check Exit Conditions
  8. Check operator load score
  9. Find ready tasks
  10. Score tasks
  11. Run Load Balancer check
  12. Dispatch safe tasks
  13. Log outputs and update Learning Log when milestones/goals complete
  14. Ask only for blockers
  15. Reroute if path is failing
```

## Layer 0 — Goal Complexity Gate

Before running any discovery or planning, compute a Goal Complexity Score:

| Signal | Points |
|---|---|
| Budget at risk > $500 or equivalent | +2 |
| Timeline > 3 months | +2 |
| Vehicle is unclear or multiple viable options exist | +3 |
| Goal requires other people or external approvals | +2 |
| Learning Log has a broken assumption in same vehicle type | +2 |

- Score **< 4 → Fast path**: confirm vehicle in one question, check operator constraints in one question, skip Phase 0-B financial stress-test, proceed to Layer 1
- Score **≥ 4 → Full path**: run Phase 0-A then Phase 0-B in sequence

## Layer 0-A — Discovery

Run Phase 0-A first. Do not generate paths or score vehicles yet. This phase only.

Research basis: HexMachina (arXiv 2506.04651) found that agents that simultaneously discover the environment and build strategy fail to stabilize. Dedicated discovery before strategy improved outcomes by 15+ percentage points.

Sequence:

1. **Clarify the true underlying outcome**
   - Look past the stated goal.
   - Example: “launch app” may really mean “financial independence by 35.”
   - Ask: “What does success actually look like in your life?”

2. **Survey the environment**
   - Is the space crowded?
   - Who are the main players?
   - Is timing favorable, neutral, or unfavorable?
   - Are there tailwinds, headwinds, dependencies, or timing constraints?

3. **Identify viable vehicle types — list only, no scoring yet**
   - Business: SaaS, services, marketplace, high-ticket, physical product
   - Employment: job, consulting, freelance
   - Investment: equity, real estate, assets
   - Hybrid combinations
   - Do not assume the stated path is the best path

4. **Document operator constraints**
   - Available capital
   - Available hours per week
   - Current skill set, honestly measured
   - Current network/distribution
   - Risk tolerance
   - Hard blockers

5. **Produce `vehicle_discovery_record`**

```json
{
  “goal_id”: “string”,
  “true_outcome”: “string”,
  “candidate_vehicles”: [“string”],
  “environment_assessment”: {
    “market_crowding”: “low | medium | high”,
    “timing”: “favorable | neutral | unfavorable”,
    “key_risks”: [“string”],
    “key_tailwinds”: [“string”],
    “overall_environment_score”: “green | yellow | red”
  },
  “operator_constraints_documented”: true,
  “status”: “stable | incomplete”,
  “source_goal_id”: “string”,
  “created_at”: “ISO date”,
  “last_updated”: “ISO date”,
  “version”: 1
}
```

**Phase 0-A Gate:** `vehicle_discovery_record.status` must be `”stable”` before proceeding to Phase 0-B.

Status is `”stable”` when all four items are complete:
1. True outcome clarified
2. Environment surveyed
3. Candidate vehicles listed
4. Operator constraints documented

If any item is missing, ask one clarifying question and wait. Do not proceed with incomplete discovery.

If `overall_environment_score` is `red`, require operator acknowledgment before moving to Phase 0-B.

## Layer 0-B — Stress-Test

Run Phase 0-B only after the Phase 0-A gate passes.

Sequence:

1. **Stress-test the math on each candidate vehicle**
   - What revenue/profit numbers are required?
   - What margins, volume, and price points does that imply?
   - What is the realistic timeline?
   - What capital, skills, or connections are prerequisites?

2. **Score each vehicle against the Operator Constraint Profile**
   - Available capital
   - Available hours per week
   - Current skill set, honestly measured
   - Current network/distribution
   - Risk tolerance
   - Hard blockers

3. **Select the best-fit vehicle or flag mismatch**
   - If achievable, proceed with the chosen vehicle
   - If unrealistic, say so clearly before building any path
   - **Never build a plan for a goal that fails its own math**

4. **Produce `vehicle_selection_record`**

```json
{
  “goal_id”: “string”,
  “true_outcome”: “string”,
  “vehicles_considered”: [
    {
      “vehicle”: “string”,
      “implied_revenue”: “string”,
      “implied_customers_or_clients”: “string”,
      “implied_timeline”: “string”,
      “prerequisite_capital”: “string”,
      “prerequisite_skills”: [“string”],
      “operator_fit_score”: “high | medium | low | mismatch”,
      “verdict”: “recommended | viable | hard | mismatch”
    }
  ],
  “selected_vehicle”: “string”,
  “selection_rationale”: “string”,
  “goal_is_realistic”: true,
  “flags”: [“string”],
  “source_goal_id”: “string”,
  “created_at”: “ISO date”,
  “last_updated”: “ISO date”,
  “version”: 1
}
```

**Phase 0-B Gate:** If `goal_is_realistic: false`, surface this to the operator clearly and do not proceed to Layer 1.

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

### Mode

Every goal has a `mode` that constrains what the agent may do autonomously:

| Mode | What the agent may do |
|---|---|
| `researcher` | Read-only: search, summarize, analyze, produce reports. No file writes, no external actions. |
| `builder` | Create and edit private files and drafts. No external communication, no deploys. |
| `engineer` | Technical work including tests, staged builds, and deploys. Level 3 actions require approval. |
| `coach` | Advise and critique only. No direct file or external actions. |

Default if not specified: `builder`. Set at goal initialization. Stored in the goal record and respected by every subagent dispatch for that goal.

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
  "status": "unvalidated | confirmed | at_risk | broken | updated",
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

### Pre-Mortem

Before finalizing exit conditions, ask the operator:

> "Imagine it's [goal deadline] and the goal failed. What is the single most likely cause?"

Use that answer to write or refine the **primary kill trigger**. This surfaces the risk the operator is already thinking about, rather than defaulting to a generic time threshold.

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
- Kill trigger: core metric [name] has not changed by more than 10% from its value at goal start, measured over any 30-day window, for 3 consecutive windows. The operator sets the threshold percentage during initialization; 10% is the default if unspecified.
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

### Priority Formula

Research basis: CLEAR (arXiv 2511.14136) found that agents optimized for task efficacy alone were 4.4–10.8x more expensive than cost-aware alternatives. Cost is integrated directly into scoring rather than handled as a separate check.

```text
score = (Reach × Impact × Confidence) ÷ (Effort × Cost_multiplier)
```

**Dimension rubrics (score 1–5):**

| Dimension | 1 | 3 | 5 |
|---|---|---|---|
| **Reach** | Unblocks 0 other tasks | Unblocks 1–2 tasks on current path | Unblocks a milestone or an entire parallel path |
| **Impact** | <5% movement on core metric | 10–25% movement on core metric | >25% movement or removes a critical blocker |
| **Confidence** | Assumption unvalidated, high impact if broken | Assumption plausible, medium impact if broken | Assumption confirmed, or impact is low regardless |
| **Effort** | >8 operator-hours | 2–8 operator-hours | <2 operator-hours |

**Cost multiplier:**

| Weekly spend position | Multiplier |
|---|---|
| Task is within weekly budget | 1.0 |
| Task pushes cumulative spend to >75% of weekly budget | 1.5 |
| Task would exhaust weekly budget | 2.0 |

**Dispatch thresholds:**
- Score ≥ 8.0: dispatch candidate
- Score 2.0–7.9: backlog
- Score < 2.0: defer or drop

### Dispatch Rules

Before dispatching any task:
1. Compute RICE score
2. Confirm score ≥ 8.0
3. Confirm task autonomy level is within approved range
4. Dispatch safe tasks
5. Gate Level 3+ actions on approval

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

## Signal Intake Layer — PCE Scoring

Run after metrics update in every loop cycle.

Research basis: PCE framework (arXiv 2602.04326) treats assumptions as first-class decision variables and scores them before metric data arrives, solving the problem that assumption breaks cause metric failures — not the reverse.

For each active assumption, run three steps:

```text
PLANNER:   What paths or milestones does this assumption enable?
           What happens to the plan if this assumption is false?

COMPOSER:  Given current evidence (completed tasks, metrics, operator updates),
           what is the likelihood this assumption still holds?
           Evidence: [list what was checked]
           likelihood: 0.0 (certainly false) → 1.0 (certainly true)

EVALUATOR: score = likelihood(0–1) × goal_directed_gain(0–1)
                   ÷ execution_cost_if_false(1–3)

           goal_directed_gain: how much does this assumption being true
             advance the core metric?
             0.0 = no effect on core metric
             1.0 = determines whether the goal succeeds

           execution_cost_if_false:
             1 = low    — can break without stopping work; easy to reroute
             2 = medium — breaking this assumption requires path reroute
             3 = critical — breaking this assumption may require killing the goal
```

Thresholds:

| Score | Action |
|---|---|
| ≥ 0.3 | Assumption healthy — continue |
| 0.1–0.3 | Flag for Strategic Review on next loop cycle |
| < 0.1 | Pause path immediately — notify operator with full assumption summary and request decision |

Update assumption `status` field:
- Score ≥ 0.3 → `confirmed` (if previously unvalidated) or `active`
- Score 0.1–0.3 → `at_risk`
- Score < 0.1 → `broken`

The PCE scoring pass replaces the deviation-percentage threshold table. It produces a score even when metrics are stale, because it reasons from available evidence rather than requiring a specific metric reading.

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

Strategy gets smarter across goals by distilling interaction trajectories into abstract, reusable principles — not by logging raw outcomes.

Research basis: EvolveR (arXiv 2510.16079) demonstrated that agents that distill trajectories into abstract principles transfer learning significantly better than agents that log raw observations.

### Two-Step Write Protocol

Run distillation when:
- A goal completes (success or kill)
- A `critical` or `high`-impact assumption breaks (PCE score < 0.1)
- A path is abandoned after a pivot trigger

**Step 1 — Trajectory record** (raw, goal-specific)

Write to `{strategy_store}/archive/trajectories.json`:

```json
{
  "trajectory_id": "string",
  "source_goal_id": "string",
  "vehicle": "string",
  "assumption_id": "string | null",
  "stated_assumption": "string",
  "actual_outcome": "string",
  "path_status_at_event": "string",
  "created_at": "ISO date",
  "last_updated": "ISO date",
  "version": 1
}
```

**Step 2 — Distilled principle** (abstract, reusable)

Write to `{strategy_store}/learning_log.json`. Before writing, check for an existing entry with the same `(source_goal_id + first 60 chars of principle)` — update rather than append if found.

```json
{
  "learning_id": "string",
  "source_goal_id": "string",
  "source_trajectory_id": "string",
  "vehicle_type": "string",
  "operator_context": "string",
  "principle": "In [vehicle type] goals with [context], [assumption type] assumptions should start at [adjusted value] until [validation milestone].",
  "confidence": "low | medium | high",
  "applicable_contexts": ["string"],
  "created_at": "ISO date",
  "last_updated": "ISO date",
  "version": 1
}
```

The `principle` field must be abstract and generalized — not a description of what happened on one goal, but a rule that would apply to a future goal in the same context.

### Retrieval at Layer 0

At every new Layer 0 run, before committing to a vehicle:

1. Query Learning Log by `vehicle_type` matching the candidate vehicles
2. Query by `operator_context` matching current operator constraints
3. Surface the top 3 most relevant principles to the operator
4. Incorporate any `high`-confidence principles into the Phase 0-B stress-test

Start empty. Do not pre-populate with invented wisdom.

## Metrics

Every goal needs at least one success metric.

Metric sources:
- `manual` — user updates it
- `file` — Strategy reads a local file
- `api` — Strategy calls an endpoint
- `derived` — calculated from other metrics
- `subagent` — reported by completed work

If metrics are stale, Strategy says so. If most metrics are stale, it avoids major reroutes and asks for updated data.

### Required Metrics: CLEAR Dimensions

Research basis: CLEAR (arXiv 2511.14136) found that agent reliability drops from ~60% to ~25% without explicit tracking, and that ignoring cost produces 4.4–10.8x waste. Every goal must track both.

In addition to the operator-defined core metric, every goal tracks:

**`cost_per_outcome`**
- Formula: `total_spend_to_date ÷ core_metric_current_value`
- Track every loop cycle
- If it increases for 3 consecutive cycles while the core metric is flat → surface a Strategic Review prompt: "Cost per unit of progress is rising while the core metric is not moving. Review the active path."

**`plan_consistency`**
- Definition: percentage of loop cycles in the last 7 where the active path and top-priority task did not change
- Track every loop cycle
- If `plan_consistency` < 40% over any 3-cycle window → surface: "Plan is changing frequently — possible oscillation. Review assumptions before next dispatch."

These are tracked automatically by the agent. They do not replace the operator-defined core metric.

## Session Start Protocol

Run this once at the start of every session. Works for both continuous agents and stateless LLMs.

```text
1. Load active goals from {strategy_store}
2. For each active goal, produce a ≤30-word status line:
   "[goal title] — [status] — top metric: [value vs target] — top blocker: [or none]"
3. If any metric source has not been updated in >7 days, surface at most
   one stale-metric question
4. Load full records only for goals with dispatched tasks or pending approvals
5. Proceed to loop — no message unless something needs operator input
```

## Communication Rules

Speak only when something changes state. Do not send messages on a clock.

| Trigger | Output |
|---|---|
| Blocker encountered | Immediate, ≤3 sentences: what is blocked, what is needed to unblock |
| Assumption PCE score drops below 0.3 | Immediate: which assumption, current score, recommended action |
| Assumption PCE score drops below 0.1 | Immediate: path paused, full assumption summary, operator decision required |
| Milestone completed | Summary: what completed, total cost to date, next ready tasks |
| Session start with no changes since last session | Silent — no message |
| Weekly (if agent runs continuously) | Review evidence, reroute, prune goals, plan next week |

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

## Memory Architecture

Strategy uses **Pattern B** memory: the agent's context window holds active working state; `{strategy_store}` holds all persistent records. Do not graduate to Pattern C (tiered with learned control) unless empirical data shows it is needed for your workload.

### Store Layout

```text
{strategy_store}/
  goals.json
  operator_profile.json
  vehicle_discovery_records.json
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
  archive/
    trajectories.json
  work/
```

### Write-Path Rules

Every record written to `{strategy_store}` must include these base fields:

```json
{
  "source_goal_id": "string",
  "created_at": "ISO date",
  "last_updated": "ISO date",
  "version": 1
}
```

Additional write-path rules — follow all of them:
- **Versioning:** Before writing an assumption update, check for an existing record with the same `assumption_id`. Increment `version`; do not create a duplicate.
- **Staleness:** When loading records, flag any record with `last_updated` > 14 days and `source: manual`. Do not silently trust stale data.
- **Deduplication:** Before writing a Learning Log entry, check for an existing entry matching `(source_goal_id + first 60 chars of distilled principle text)`. If a near-duplicate exists, update it rather than append.
- **Canonicalization:** Do not append raw interaction output verbatim. Summarize and canonicalize before storing (see Learning Log section).

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

**v3 additions:**
- [ ] Runtime Adapter section present; no `~/.hermes/` or platform-specific paths in skill body
- [ ] Write-path rules documented: version field, dedup check, staleness flag, canonicalization requirement
- [ ] Session start protocol replaces morning/evening rhythm
- [ ] Event-driven communication table replaces clock-based cadence
- [ ] Four mode types defined with explicit behavioral contracts
- [ ] Layer 0 Complexity Gate with fast path (< 4) and full path (≥ 4) documented
- [ ] Layer 0 split into Phase 0-A (Discovery) and Phase 0-B (Stress-Test) with gate between them
- [ ] PCE scoring format (PLANNER / COMPOSER / EVALUATOR) replaces deviation-percentage Signal Intake table
- [ ] PCE thresholds defined: ≥ 0.3 (healthy), 0.1–0.3 (flag), < 0.1 (pause + notify)
- [ ] `at_risk` is a valid assumption status
- [ ] Learning Log uses two-step distillation: trajectory to archive, principle to learning_log
- [ ] Learning Log retrieval at Layer 0 queries by `vehicle_type` and `operator_context`
- [ ] RICE formula present with rubrics (1 / 3 / 5 anchors per dimension)
- [ ] Cost multiplier (1.0 / 1.5 / 2.0) integrated into RICE, Load Balancer section removed
- [ ] Pre-mortem step added to exit condition initialization
- [ ] Kill trigger default uses specific percentage (10%), window (30 days), and consecutive count (3)
- [ ] `cost_per_outcome` and `plan_consistency` added as required metric types
- [ ] `plan_consistency` < 40% triggers oscillation warning

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
