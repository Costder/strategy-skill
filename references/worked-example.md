# Strategy Skill -- Worked Example

This section traces a single goal from raw input through Layer 0, Layer 1, Layer 2, Layer 3, and one PCE loop cycle. Real numbers are used throughout. The stress-test rejects one vehicle on math grounds. The PCE pass catches a failing assumption early.

---

### Input

```text
/strategy Reach $5,000/month in recurring revenue within 6 months,
starting from about $0 capital and ~10 hours per week.
```

---

### Layer 0 -- Complexity Gate

Before any discovery, compute the Goal Complexity Score:

| Signal | Points | Applies? |
|---|---|---|
| Budget at risk > $500 | +2 | No (~$0 capital) |
| Timeline > 3 months | +2 | Yes (6 months) |
| Vehicle unclear or multiple viable options | +3 | Yes (SaaS, services, community, content all viable) |
| Requires other people or external approvals | +2 | No |
| Learning Log: broken assumption in same vehicle type | +2 | No (log is empty) |

Total = **5**. Score >= 4 -> **Full path**: run Phase 0-A then Phase 0-B.

---

### Phase 0-A -- Discovery

```text
Discovery questions and answers:

Q: What does success actually look like in your life?
A: Build a durable source of independent income and prove I can run a
   product business -- not just hit a vanity MRR number once.

Q: What is your available capital, hours, skills, and network?
A: ~$0 liquid capital available for this. 10 hours per week.
   Skills: full-stack dev, basic copywriting.
   Network: thin -- no audience, no email list.

Q: What hard blockers apply?
A: Keep day job. No paid ads until revenue funds them.
```

**Environment scan:**

| Factor | Assessment |
|---|---|
| Market crowding | High -- SaaS and services markets are full |
| Timing | Neutral -- no special window open or closing |
| Key risks | No existing audience or reach; only 10 hrs/week; SaaS has long time-to-revenue |
| Key tailwinds | AI lowers build cost; underserved niches exist for specialists |
| Overall environment score | Yellow |

**Candidate vehicles identified (list only -- no scoring yet):**
- niche B2B SaaS
- productized service
- paid community / cohort
- content + affiliate

**vehicle_discovery_record:**

```json
{
  "goal_id": "G1",
  "true_outcome": "Build a durable source of independent income and prove I can run a product business -- not just hit a vanity MRR number once.",
  "candidate_vehicles": [
    "niche B2B SaaS",
    "productized service",
    "paid community/cohort",
    "content + affiliate"
  ],
  "environment_assessment": {
    "market_crowding": "high",
    "timing": "neutral",
    "key_risks": [
      "no existing audience or reach",
      "only 10 hrs/week",
      "SaaS has long time-to-revenue"
    ],
    "key_tailwinds": [
      "AI lowers build cost",
      "underserved niches exist"
    ],
    "overall_environment_score": "yellow"
  },
  "operator_constraints_documented": true,
  "status": "stable",
  "source_goal_id": "G1",
  "created_at": "2026-06-06",
  "last_updated": "2026-06-06",
  "version": 1
}
```

```text
Phase 0-A Gate: status = "stable" -- all four items complete.
overall_environment_score = "yellow" -- no operator acknowledgment required.
Proceed to Phase 0-B.
```

---

### Phase 0-B -- Stress-Test

Each vehicle is stress-tested against the math and the Operator Constraint Profile.

**Operator Constraint Profile:**

```json
{
  "operator_id": "operator-1",
  "available_capital": 500,
  "available_hours_per_week": 10,
  "current_skills": ["full-stack dev", "basic copywriting"],
  "current_network": "thin -- no audience or email list",
  "risk_tolerance": "medium",
  "hard_constraints": ["keep day job", "no paid ads until revenue funds them"],
  "active_goals": ["G1"],
  "current_load_score": 1
}
```

**Math stress-test per vehicle:**

| Vehicle | Implied customers | Implied price | Implied timeline | Capital needed | Operator fit |
|---|---|---|---|---|---|
| niche B2B SaaS | ~100 paying users | ~$50/mo | 9-12 months to $5K | Low to build, needs distribution | Medium |
| paid-ads-driven SaaS | ~100 paying users | ~$50/mo | Unknown | Thousands in ad spend (LTV ~$300, CAC must be funded up front) | Mismatch |
| productized service | ~5 clients | ~$1,000/mo (or 10 @ $500) | 2-4 months to first clients | ~$0 | High |
| paid community/cohort | ~100 members | ~$50/mo | Needs existing audience first | Low | Low |

**Why paid-ads-driven SaaS is rejected on math:**

```text
Target MRR: $5,000
LTV per customer at $50/mo (12-month churn ~50%): ~$300
CAC must be less than LTV to be profitable.
But CAC must be funded up front in cash before any revenue returns.
Available capital: ~$0.
This vehicle cannot close the math. Reject.
```

**vehicle_selection_record:**

```json
{
  "goal_id": "G1",
  "true_outcome": "Build a durable source of independent income and prove I can run a product business -- not just hit a vanity MRR number once.",
  "vehicles_considered": [
    {
      "vehicle": "niche B2B SaaS",
      "implied_revenue": "$5K/mo",
      "implied_customers_or_clients": "~100 paying @ $50/mo",
      "implied_timeline": "9-12 months to $5K, not 6",
      "prerequisite_capital": "low to build, but needs distribution",
      "prerequisite_skills": ["product", "dev"],
      "operator_fit_score": "medium",
      "verdict": "hard"
    },
    {
      "vehicle": "paid-ads-driven SaaS",
      "implied_revenue": "$5K/mo",
      "implied_customers_or_clients": "~100 @ $50/mo",
      "implied_timeline": "unknown",
      "prerequisite_capital": "thousands in ad spend (LTV ~$300, CAC must be funded up front)",
      "prerequisite_skills": ["paid acquisition"],
      "operator_fit_score": "mismatch",
      "verdict": "mismatch"
    },
    {
      "vehicle": "productized service",
      "implied_revenue": "$5K/mo",
      "implied_customers_or_clients": "~5 clients @ $1K/mo (or 10 @ $500)",
      "implied_timeline": "2-4 months to first paying clients",
      "prerequisite_capital": "~$0",
      "prerequisite_skills": ["delivery skill already held", "outreach"],
      "operator_fit_score": "high",
      "verdict": "recommended"
    },
    {
      "vehicle": "paid community/cohort",
      "implied_revenue": "$5K/mo",
      "implied_customers_or_clients": "~100 members @ $50/mo",
      "implied_timeline": "needs an existing audience first",
      "prerequisite_capital": "low",
      "prerequisite_skills": ["audience"],
      "operator_fit_score": "low",
      "verdict": "hard"
    }
  ],
  "selected_vehicle": "productized service first, as an on-ramp; reinvest cash + niche insight into a niche SaaS later",
  "selection_rationale": "Service closes the 6-month math -- 5 clients is reachable, while SaaS needs ~100 customers and 9-12 months. Service also funds the work and produces the niche insight that de-risks a later SaaS.",
  "goal_is_realistic": true,
  "flags": [
    "$5K/mo via SaaS alone in 6 months from zero audience is not realistic",
    "paid acquisition is off the table at current capital",
    "reach/distribution is the binding constraint, not the ability to build"
  ],
  "source_goal_id": "G1",
  "created_at": "2026-06-06",
  "last_updated": "2026-06-06",
  "version": 1
}
```

```text
Phase 0-B Gate: goal_is_realistic = true. Proceed to Layer 1.
```

---

### Layer 1 -- Goal Initialization

**5 setup questions:**

```text
1. What outcome do you want?
   Reach $5,000/month in recurring revenue.

2. By when?
   Within 6 months -- by 2026-12-06.

3. How will we measure success?
   MRR tracked manually each month. Paying client count tracked manually.

4. What should I never do without asking?
   Send any outreach messages, publish anything publicly, spend money,
   or commit to any client work on my behalf.

5. What tools/accounts/files can I use?
   Local files, web search, draft documents. No external accounts
   without explicit approval.
```

**Goal record:**

```json
{
  "goal_id": "G1",
  "title": "Reach $5K/month recurring within 6 months",
  "deadline": "2026-12-06",
  "mode": "builder",
  "selected_vehicle": "productized service (on-ramp to SaaS)",
  "metrics": {
    "mrr": {"current": 0, "target": 5000, "source": "manual"},
    "paying_clients": {"current": 0, "target": 5, "source": "manual"}
  },
  "paths": ["P1"],
  "approval_policy": "standard",
  "status": "active"
}
```

**Assumption Registry (3 assumptions required before tasks are generated):**

```json
[
  {
    "assumption_id": "A1",
    "goal_id": "G1",
    "path_id": "P1",
    "statement": "A specific niche (Shopify app developers) will pay $1,000/mo for a done-for-you service.",
    "type": "demand",
    "assumed_value": "$1,000/mo per client",
    "actual_value": null,
    "status": "unvalidated",
    "last_checked": "2026-06-06",
    "impact_if_broken": "high"
  },
  {
    "assumption_id": "A2",
    "goal_id": "G1",
    "path_id": "P1",
    "statement": "Cold outreach converts at >= 3% to a discovery call.",
    "type": "conversion",
    "assumed_value": ">= 3% reply-to-call rate",
    "actual_value": null,
    "status": "unvalidated",
    "last_checked": "2026-06-06",
    "impact_if_broken": "high"
  },
  {
    "assumption_id": "A3",
    "goal_id": "G1",
    "path_id": "P1",
    "statement": "One operator can deliver 5 concurrent service clients within 10 hrs/week using templates.",
    "type": "skill",
    "assumed_value": "5 clients deliverable at 10 hrs/week",
    "actual_value": null,
    "status": "unvalidated",
    "last_checked": "2026-06-06",
    "impact_if_broken": "medium"
  }
]
```

**Exit Conditions -- Pre-Mortem first:**

```text
Q: Imagine it is month 6 and the goal failed.
   What is the single most likely cause?

A: I kept polishing the offer but never did consistent outreach,
   so I never had enough sales conversations.
```

That answer keys the primary kill trigger to outreach volume, not just MRR.

```json
{
  "exit_conditions": {
    "kill_triggers": [
      {
        "metric": "discovery_calls_booked",
        "condition": "fewer than",
        "threshold": "4 per month",
        "evaluation_window_days": 30
      }
    ],
    "pivot_triggers": [
      {
        "metric": "mrr",
        "condition": "under",
        "threshold": "$1,000 (20% of target) after month 3",
        "evaluation_window_days": 30
      }
    ],
    "max_budget": 500,
    "max_timeline_days": 180,
    "paths_exhausted_action": "escalate_to_operator"
  }
}
```

---

### Layer 2 -- Paths, Milestones, Tasks

**Path P1:** Land first $2K MRR in the productized service.

**Milestones:**
- **M1** -- Offer defined + 3 paying clients
- **M2** -- Delivery systematized, reach $2K MRR

**Tasks:**

```json
[
  {
    "task_id": "G1-P1-T1",
    "title": "Define the niche and write the productized offer (scope, price, promise) as a one-page sales doc",
    "department": "product",
    "status": "ready",
    "autonomy_level": 1,
    "depends_on": [],
    "deliverable": "offer-one-pager.md",
    "success_metric": "offer_ready",
    "estimated_cost": 0,
    "estimated_hours": 3,
    "priority": null
  },
  {
    "task_id": "G1-P1-T2",
    "title": "Build a 40-prospect outreach list in the niche with contact and one personalization hook each",
    "department": "growth",
    "status": "ready",
    "autonomy_level": 1,
    "depends_on": ["G1-P1-T1"],
    "deliverable": "outreach-list.md",
    "success_metric": "list_ready",
    "estimated_cost": 0,
    "estimated_hours": 4,
    "priority": null
  },
  {
    "task_id": "G1-P1-T3",
    "title": "Draft 10 personalized outreach messages",
    "department": "growth",
    "status": "backlog",
    "autonomy_level": 1,
    "depends_on": ["G1-P1-T2"],
    "deliverable": "10 drafts in outreach-drafts.md",
    "success_metric": "drafts_ready",
    "estimated_cost": 0,
    "estimated_hours": 2,
    "priority": null
  }
]
```

```text
Note on T3: drafting the messages is Level 1 (private execution).
Sending them is Level 3 (external communication) and is approval-gated.
The subagent produces drafts only. Sending requires explicit operator sign-off.
```

---

### Layer 3 -- Scoring and Dispatch

**Score T2 (outreach list) using the priority formula:**

```text
score = (Reach x Impact x Confidence) / (Effort x Cost_multiplier)
```

| Dimension | Score | Rationale |
|---|---|---|
| Reach | 5 | Unblocks the entire outreach path (T3, discovery calls, and all downstream tasks) |
| Impact | 4 | Directly feeds the binding constraint: reach/distribution |
| Confidence | 5 | List-building is well understood; low assumption risk |
| Effort | 3 | Estimated 4 hours -- falls in the 2-8 hr band |
| Cost_multiplier | 1.0 | Within weekly budget (no spend required) |

```text
score = (5 x 4 x 5) / (3 x 1.0)
      = 100 / 3
      = 33.3

33.3 >= 8.0 -> dispatch candidate.
```

**Resulting /goal packet dispatched to subagent:**

```text
/goal Build the 40-prospect outreach list for the [niche] productized service.

Success means:
- 40 prospects in the target niche
- each row has name, company, role, a verified contact, and one personalization hook
- saved as outreach-list.md
- no messages sent (sending is approval-gated)

Stop if blocked by missing access to a contact-finding tool or an unclear niche.
```

---

### One Loop Cycle Later -- PCE Check on A2

After the list is built, 20 outreach messages are sent (operator approved). Zero replies.

**PCE scoring for assumption A2** ("Cold outreach converts at >= 3% to a discovery call"):

```text
PLANNER:   A2 enables the entire reach -> revenue path.
           If A2 is false, the pipeline never fills with discovery calls.
           No calls means no clients. No clients means MRR stays at $0.

COMPOSER:  Evidence: 20 messages sent, 0 replies. At 3% that predicts ~0.6 replies,
           so 0 is weak evidence against A2, not proof.
           Likelihood A2 still holds: ~0.75  ->  p_false = 0.25

EVALUATOR: A2 impact_if_broken = high  ->  cost_weight = 3
           validation_priority = p_false x cost_weight = 0.25 x 3 = 0.75   (rank it for testing)
           health: high-impact pauses at p_false >= 0.30; flag band is 0.20-0.30.
                   p_false 0.25 falls in the flag band.
```

```text
p_false 0.25 sits in the flag band for a high-impact assumption.
Action: set A2 status = "at_risk". Flag for Strategic Review on next loop cycle.
Recommended action: test a different channel or rewrite the message before scaling outreach.
Note: because A2 is high-impact it flags at a low p_false (pause at 0.30); a low-impact
assumption would not flag until p_false >= 0.70. That impact-scaling is the v3.1 fix.
```

---

### What This Example Shows

The skill rejected the paid-ads-driven SaaS vehicle because the math cannot close at $0 capital. It picked the productized service because 5 clients is reachable and the capital requirement matches. It caught A2 going at-risk after just 20 data points -- before the operator spent weeks sending messages that would never convert.

That is the core value: reject the doomed path early, pick the one that closes the math, and surface failing assumptions before they waste months of work.
