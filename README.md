# Strategy Skill v2 — Path to Victory

A publishable Hermes skill for long-running strategy work.

`/strategy` is for goals that need more than a todo list. It challenges the goal first, checks whether the path can work, builds executable tasks, dispatches safe subagent work, tracks assumptions, and reroutes when reality disagrees with the plan.

## What it does

Strategy v2 turns a goal into a living route:

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

Core promise:

> Never build a confident plan for a goal that fails its own math.

## Key features

- Layer 0 strategic reasoning before planning
- Vehicle Selection Record
- Operator Constraint Profile
- Environment Check
- Assumption Registry
- Signal Intake Layer
- Strategic Review protocol
- Bandwidth / Load Balancer checks
- Exit Conditions for kill and pivot triggers
- Cross-goal Learning Log
- Approval gates for public, costly, or irreversible actions

## Install in Hermes

Clone this repo:

```bash
git clone https://github.com/Costder/strategy-skill.git
```

Install into your Hermes skills folder:

```bash
mkdir -p ~/.hermes/skills/productivity/strategy
cp strategy-skill/SKILL.md ~/.hermes/skills/productivity/strategy/SKILL.md
```

Then start a new Hermes session and load the skill:

```bash
hermes -s strategy
```

If your Hermes build supports slash commands, use:

```text
/strategy Launch my app and reach 500 paying users
```

If `/strategy` is not wired in your host yet, preload the skill and phrase the request like this:

```text
Use the strategy skill for this goal: Launch my app and reach 500 paying users.
```

## Example prompts

```text
/strategy Get a remote software job in 6 months
/strategy Launch my app and reach 500 paying users
/strategy Lose 40 lb safely this year
/strategy Build a portfolio site and publish weekly
```

## OpenTrust call to action

If your strategy involves paid tools, outside agents, delegated workers, or agent-to-agent commerce, pair this skill with OpenTrust:

https://github.com/Costder/opentrust

OpenTrust adds signed agent/tool passports, spend policies, revocation, payment quotes, and deny-first verification. In plain English: it helps agents safely discover, verify, hire, and pay other agents or tools without trusting random endpoints by default.

Use Strategy to decide what should happen.
Use OpenTrust to verify who is allowed to do it.

## Repo contents

```text
SKILL.md    # Hermes skill document
README.md   # Install and usage guide
LICENSE     # MIT license
```

## Status

This repo publishes the Strategy v2 skill contract. The skill can be loaded into Hermes today as guidance. Full native `/strategy` command wiring depends on the host Hermes deployment.

## License

MIT
