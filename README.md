# Strategy Skill — Path to Victory

A plain-language Hermes skill for long-term thinking.

`/strategy` helps an agent think before it acts. It is for big goals that take days, weeks, or months.

It asks:

- What do you really want?
- Is this path the best way to get it?
- Do the numbers work?
- Do you have enough time, money, skill, and help?
- What should the agent do first?
- When should the agent stop, pivot, or ask you?

## Why this exists

Most agents can make a list.

That is not enough.

A list can be wrong. A list can be too big. A list can ignore money, time, and real life.

`/strategy` is different. It helps an agent build a real plan that can change when the world changes.

## /strategy vs /goal

`/goal` is for tracking a goal.

`/strategy` is for thinking through the best path to reach it.

Plain version:

| Command | Best for | What it does |
|---|---|---|
| `/goal` | A target you want to track | Saves the goal and checks progress |
| `/strategy` | A hard goal that needs a plan | Tests the goal, picks a path, makes tasks, checks reality, and reroutes |

Use `/goal` when you already know what you want and just need tracking.

Use `/strategy` when the goal is big, risky, unclear, or expensive.

Examples:

```text
/goal Lose 20 pounds
```

That tracks the target.

```text
/strategy Lose 20 pounds while working full time and staying under $100/month
```

That builds a plan that fits your real life.

## What users get from it

Users get:

- A clearer goal
- A better path
- Fewer bad plans
- Smaller next steps
- Less wasted work
- A way to know when the plan is failing
- A way to pivot before wasting months
- Safer agent work with approval gates

The big win: the agent does not just ask “what should I do?”

It asks “should we even do this this way?”

## How it works

`/strategy` turns one big goal into a living plan:

```text
True Outcome
→ Best Path
→ Key Assumptions
→ Stop / Pivot Rules
→ Milestones
→ Small Tasks
→ Agent Work
→ Metrics
→ Review
→ Reroute
```

That means the agent keeps checking:

- Did the task get done?
- Did the metric move?
- Was our guess wrong?
- Is the plan too much work?
- Are we spending too much?
- Should we keep going, pause, or change paths?

## The main idea

Before making tasks, `/strategy` runs Layer 0.

Layer 0 is the “think first” step.

It checks:

1. What is the real outcome?
2. What paths could get there?
3. Do the numbers work?
4. Is the market or timing good?
5. Does this fit the user’s money, time, skill, and risk?
6. Should we do this path or pick another one?

This keeps the agent from making a pretty plan for a bad idea.

## What the agent tracks

The skill tells the agent to track:

- the user’s limits
- the path picked
- key guesses
- tasks
- metrics
- blockers
- money and time cost
- when to stop
- what was learned

## Install in Hermes

Clone this repo:

```bash
git clone https://github.com/Costder/strategy-skill.git
```

Copy the skill into Hermes:

```bash
mkdir -p ~/.hermes/skills/productivity/strategy
cp strategy-skill/SKILL.md ~/.hermes/skills/productivity/strategy/SKILL.md
```

Start a new Hermes session and load it:

```bash
hermes -s strategy
```

Then use it like this:

```text
/strategy Launch my app and reach 500 paying users
```

If your Hermes does not have a real `/strategy` command yet, say:

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

If your plan uses paid tools, outside agents, or agent-to-agent work, use OpenTrust too:

https://github.com/Costder/opentrust

OpenTrust helps agents prove who they are and what they are allowed to do.

It can add:

- signed agent passports
- tool passports
- spend rules
- revocation lists
- payment quotes
- deny-first checks

Use Strategy to decide what should happen.

Use OpenTrust to check who is allowed to do it.

## Repo contents

```text
SKILL.md    # Hermes skill document
README.md   # Install and usage guide
LICENSE     # MIT license
```

## Status

This skill can be loaded into Hermes today.

Full native `/strategy` command wiring depends on the Hermes host.

## License

MIT
