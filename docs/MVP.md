# MVP and Validation Plan

## 1. Do not start with the full vision

The full concept implies:

- Windows;
- macOS;
- Android;
- iOS;
- browser extensions;
- wearables;
- calendar;
- task integrations;
- always-on sensing;
- intervention learning;
- security policy infrastructure.

Building everything first would validate engineering ability rather than product demand.

The MVP should isolate the key behavioral hypothesis.

---

# 2. MVP hypothesis

> Context-aware accountability produces better adherence to self-approved plans than planning and reminders alone.

---

# 3. MVP scope

Recommended:

```text
Desktop app
+
browser extension
+
calendar
+
AI roadmap
+
activity classification
+
intervention engine
```

One primary goal per user.

Duration:

```text
30 days
```

---

# 4. MVP onboarding

User enters:

```text
"I want to..."
```

AI interview collects:

- goal;
- why;
- deadline;
- weekly availability;
- current obligations;
- hobbies / entertainment;
- protected time;
- preferred strictness.

Then generates:

```text
Goal Contract
+
30-day roadmap
+
week 1 plan
```

User approves.

---

# 5. Activity sensing

Desktop:

- foreground application;
- idle state;
- browser domain;
- category classification.

Categories:

```text
goal_work
work
communication
research
entertainment
social
gaming
system
unknown
```

Do not collect page contents for the first MVP.

---

# 6. Core states

The system needs only a few useful states.

```text
ON_PLAN
OFF_PLAN_SHORT
OFF_PLAN_REPEATED
PLANNED_LEISURE
UNAVAILABLE
BREAK
UNKNOWN
```

Avoid overcomplicated psychological inference.

---

# 7. Three strictness modes

## Coach

Notification only.

## Guardrail

Notification + friction.

## Contract

Temporary user-preapproved blocking.

The MVP should measure how users move between modes.

---

# 8. Daily screen

Only:

```text
TODAY

[ ] Task 1
[ ] Task 2
[ ] Task 3

Protected leisure:
20:00–22:00
```

Avoid feature bloat.

---

# 9. Intervention examples

## Subtle

> You planned to work on the portfolio until 15:00. Continue the break or return?

## Motivation-linked

> You said shipping this project matters because you want a demonstrable AI portfolio. Start with 10 minutes?

## Friction

> Entertainment has been open for 18 minutes during your focus block.

Buttons:

```text
Return to task
Take deliberate 15-min break
Change today's plan
Continue anyway
```

The last option matters.

The system should learn from it.

---

# 10. Weekly review

Example:

```text
Week 2

Commitments completed       74%
Planned leisure respected   91%
Focus time                  8h 42m
Interventions               17
Ignored                     5

Most effective:
10-minute starter

Most common blocker:
starting complex tasks after 17:00

Suggested change:
move project work to 11:00–13:00
```

---

# 11. Metrics

## Primary metric

```text
Commitment Completion Rate (CCR)

completed self-approved commitments
-----------------------------------
all self-approved commitments
```

## Secondary

### Intervention acceptance

```text
accepted interventions / total interventions
```

### Override rate

```text
explicit overrides / restrictive interventions
```

### Notification efficiency

```text
successful interventions / prompts
```

### Planned leisure integrity

Does the system leave approved entertainment alone?

### Replan frequency

How often does reality force plan changes?

### Retention

Day 7 / 14 / 30.

### Perceived autonomy

Short validated survey items should be considered in research trials.

### Irritation

Simple recurring measurement:

```text
"Did the system annoy you today?"
1–5
```

---

# 12. What success looks like

The MVP is promising if users:

- complete more self-approved commitments;
- keep using it for multiple weeks;
- do not experience escalating notification fatigue;
- keep planned leisure intact;
- increasingly require fewer interventions for stable behaviors.

---

# 13. Failure conditions

The concept may fail if:

- users frequently disable monitoring;
- interventions become background noise;
- users manipulate activity detection;
- roadmap quality is poor;
- users constantly override restrictions;
- the system damages planned leisure;
- privacy cost feels larger than accountability benefit.

These are product findings, not merely bugs.

---

# 14. Development phases

## Phase 0 — clickable prototype

Validate:

- Goal Contract UX;
- roadmap review;
- daily screen;
- intervention language.

## Phase 1 — desktop telemetry

Implement:

- active app detection;
- idle detection;
- browser domain classification.

## Phase 2 — closed loop

Add:

- plan alignment;
- interventions;
- basic outcomes.

## Phase 3 — personalization

Add:

- intervention effectiveness model;
- adaptive timing;
- adaptive strictness recommendations.

## Phase 4 — phone

Only after desktop value is demonstrated.

## Phase 5 — multi-device Life OS

Add:

- mobile sensing;
- wearables;
- richer context;
- shared accountability;
- more life domains.

---

# 15. Recommended technical direction

Possible architecture:

```text
Desktop:
Tauri / native service

Browser:
Chrome/Firefox extension

Backend:
Python / FastAPI

DB:
Postgres

Realtime:
WebSocket / event bus

Local event storage:
SQLite

Policy:
deterministic rules / OPA-style engine

AI:
LLM planner + structured tool calling

Embeddings / memory:
only if needed after MVP
```

Important:

Do not make the LLM the policy engine.

---

# 16. Initial backlog

### P0

- goal onboarding;
- Goal Contract;
- roadmap generation;
- calendar planning;
- foreground app tracking;
- browser category;
- planned leisure;
- daily view;
- coach interventions;
- weekly report.

### P1

- Guardrail mode;
- blocker rules;
- intervention effectiveness statistics;
- fallback actions;
- automatic replanning.

### P2

- Contract mode;
- accountability partner;
- mobile companion;
- wearable signals.

---

# 17. North-star principle

The system wins when the user can say:

> "It helps me do what I already decided matters to me."

Not:

> "It decides how I should live."
