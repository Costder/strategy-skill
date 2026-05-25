# Strategy Skill — Path to Victory

A plain-language Hermes skill for long-term agent thinking.

`/strategy` helps an agent pick the right path before it starts working.

It is not a replacement for `/goal`.

`/goal` is the engine that keeps an agent moving.

`/strategy` is the map that tells the agent where to go, why that path makes sense, when to stop, and when to change direction.

## What this repo is

This repo ships a Hermes `SKILL.md` file.

That means it gives an agent clear rules for how to think and plan.

It does not, by itself, install a native slash command into every Hermes build.

If your Hermes host has a real `/strategy` command wired in, you can use that.

If not, load the skill and say:

```text
Use the strategy skill for this goal: [your goal]
```

That is the honest public status:

```text
Skill behavior: yes
Native /strategy command everywhere: no
Full background strategy engine: no
```

## Why this skill exists

Agents are good at doing work.

That can be dangerous.

If the goal is wrong, the agent may work very hard on the wrong thing.

`/strategy` slows the agent down at the start so it can ask:

- What does the user really want?
- Is this the right goal?
- What path has the best chance to work?
- What proof would show it is working?
- What should make us stop?
- What should make us change the plan?
- How much time, money, or energy can the user spend?

Then it turns the answer into a clear plan.

After that, the agent can turn parts of the plan into `/goal` prompts, tasks, subagent jobs, or normal tool work.

## `/goal` vs `/strategy`

Hermes `/goal` and Codex `/goal` use the Ralph-loop idea.

A Ralph loop means:

- you give the agent one clear target
- the agent keeps working across turns
- a judge or goal state checks if the work is done
- if not done, the agent keeps going
- it stops when done, paused, blocked, or out of budget

That is useful.

But it assumes the target is already the right target.

`/strategy` does a different job.

It helps decide what target should be given to `/goal` in the first place.

| Tool | What it is for | Best when |
|---|---|---|
| `/goal` | Keep working until one clear job is done | You know the job, the stop rule, and how to test it |
| `/strategy` | Think through the best long-term path | The goal is big, risky, unclear, expensive, or may take weeks |

Simple way to think about it:

```text
/goal = keep going until this job is done
/strategy = decide which job is worth doing, why, and when to change course
```

Another way:

```text
/goal is the engine.
/strategy is the steering wheel, map, dashboard, and brake.
```

## When to use `/goal`

Use `/goal` when the work is clear.

Good examples:

```text
/goal Fix the failing tests and verify they pass.
/goal Migrate this feature and keep the UI the same.
/goal Build the app in PLAN.md and run the checks.
```

These are good `/goal` jobs because the agent can know what done means.

## When to use Strategy

Use Strategy when the goal needs thought before action.

Good examples:

```text
Use the strategy skill for this goal: Help me grow my app to 1,000 paying users.
Use the strategy skill for this goal: Help me decide what product to build next.
Use the strategy skill for this goal: Help me turn my messy business idea into a real plan.
Use the strategy skill for this goal: Help me pick the best path to make $10k/month.
Use the strategy skill for this goal: Help me choose what agents should work on this week.
```

If your host has `/strategy` wired in, the same ideas can be written as:

```text
/strategy Help me grow my app to 1,000 paying users.
```

These are strategy jobs because the best path is not obvious yet.

## What Strategy gives the user

Strategy gives the user:

- a clearer goal
- a better path
- fewer bad plans
- better use of time
- better use of money
- fewer wasted agent runs
- a clear stop rule
- a clear change-plan rule
- a plan that can feed into `/goal`
- a learning log pattern so future plans can get smarter

The big win:

```text
/goal helps the agent finish work.
/strategy helps the agent choose the right work.
```

## How Strategy works

The skill tells the agent to turn a big wish into a living plan.

It uses these layers:

1. Find the true outcome.
2. Pick the best vehicle.
3. Check the math.
4. Check the user’s limits.
5. Write the assumptions.
6. Set kill and pivot rules.
7. Break the path into tasks.
8. Decide what should be done by the main agent, subagents, or `/goal`.
9. Check signals over time.
10. Change the plan when reality changes.
11. Save lessons for the next goal.

A plain skill install gives the agent this process.

A deeper host integration can also add persistent files, dashboards, background loops, and real `/strategy` commands.

## What is a vehicle?

A vehicle is the path used to reach the outcome.

Example:

```text
Outcome: make more money
Bad plan: just work harder
Possible vehicles:
- build a product
- sell a service
- grow an audience
- get a better job
- buy ads
- build a partner channel
```

Strategy helps the agent choose the vehicle before it starts doing work.

This matters because a bad vehicle can waste months.

## How Strategy can use `/goal`

Strategy can create a clean `/goal` packet.

Example:

```text
Strategy goal:
Grow my app to 1,000 paying users.
```

Strategy thinks first.

Then it may create this work packet:

```text
/goal Build and test the first landing page experiment.
Success means:
- page is live
- analytics are installed
- signup button works
- copy matches the chosen audience
- test plan is written
Stop if blocked by missing domain or account access.
```

That is the right split.

Strategy chooses the path.

`/goal` executes one clear piece of the path.

## Install

Clone this repo:

```bash
git clone https://github.com/Costder/strategy-skill.git
```

Install into Hermes:

```bash
mkdir -p ~/.hermes/skills/productivity/strategy
cp strategy-skill/SKILL.md ~/.hermes/skills/productivity/strategy/SKILL.md
```

Restart Hermes or reload skills.

Then use:

```text
Use the strategy skill for this goal: Help me choose the best path to reach my goal.
```

If your Hermes build has a real `/strategy` slash command, you can also use:

```text
/strategy Help me choose the best path to reach my goal.
```

## OpenTrust

If your agents use paid tools, outside workers, marketplaces, or shared budgets, pair Strategy with OpenTrust.

OpenTrust helps agents prove who they are, what they can do, what they may spend, and how they should be paid.

Build the trust layer for agent work here:

https://github.com/Costder/opentrust

Call to action:

```text
Star OpenTrust, try it with agent workflows, and help make agent trust and payments an open standard.
```

## Example start

```text
Use the strategy skill for this goal: I want to build a small online business that can make $5k/month within 6 months.
```

The agent should not start by making a todo list.

It should first ask:

```text
What outcome do you really want?
What paths could reach it?
What proof would show progress?
What limits do you have?
What would make this plan fail?
When should we stop or pivot?
```

Then it can plan.

Then it can hand clear jobs to `/goal` or other agents.

## License

MIT
