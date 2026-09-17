# Product Specification

## 1. Problem

People regularly create goals during high-motivation periods but make daily decisions in very different contexts.

Traditional systems have several gaps:

- calendars know time but not intent;
- to-do apps know tasks but not actual behavior;
- habit trackers record completion but usually do not understand context;
- blockers can prevent behavior but often lack connection to higher-level goals;
- general-purpose AI can make plans but normally does not close the loop with real-world execution.

The product hypothesis is that a system can improve goal execution by linking:

**long-term intent → concrete plans → observed behavior → context-aware intervention → adaptation.**

---

## 2. Product objective

Create a personal AI execution system that helps a user consistently follow self-approved goals while preserving autonomy, planned leisure, recovery, and changing life constraints.

The system should optimize for:

```text
goal progress
+ plan adherence
+ sustainable workload
+ intentional leisure
+ recovery
+ user autonomy
```

rather than:

```text
maximum work hours
or
maximum app engagement
```

---

## 3. Goal onboarding

The AI should not immediately turn a sentence into tasks.

It first performs a **Goal Interview**.

Example questions:

- What exactly do you want?
- Why does it matter?
- What does success look like?
- What is the deadline?
- What resources already exist?
- What constraints exist?
- How much weekly time is acceptable?
- What must not be sacrificed?
- What hobbies / entertainment / relationships should remain protected?
- What types of intervention are acceptable?

The result becomes a draft **Goal Contract**.

---

## 4. Goal Contract

A Goal Contract is a machine-readable and human-readable object containing:

- desired outcome;
- deadline;
- milestones;
- allowed weekly workload;
- protected time;
- minimum sleep / recovery constraints if the user chooses to include them;
- entertainment allowance;
- acceptable intervention types;
- accountability settings;
- permissions granted to the agent;
- conditions under which the AI may replan automatically;
- conditions requiring explicit approval.

Example:

```yaml
goal:
  title: "Ship MVP"
  deadline: "2026-11-30"

constraints:
  max_deep_work_per_day: "4h"
  minimum_sleep_target: "7h"
  protected_evenings:
    - "Friday"

leisure:
  gaming:
    weekly_budget: "8h"
    protected: true

enforcement:
  default_mode: "guardrail"
  allow_app_friction: true
  allow_hard_blocking: false
  accountability_partner: optional
```

The AI can propose the contract.

The user approves it.

---

## 5. Roadmap generation

The roadmap should contain four levels:

```text
Goal
└── Milestone
    └── Weekly outcome
        └── Action
```

Every action should ideally include:

- expected duration;
- context;
- dependency;
- priority;
- definition of done;
- evidence of completion;
- fallback version.

Example:

```text
Goal: Get an AI automation job

Milestone:
Portfolio is interview-ready

Weekly outcome:
Publish one demonstrable agent project

Action:
Record a 3-minute demo

Fallback:
Record an unedited 60-second proof-of-work clip
```

Fallback actions are important because they reduce all-or-nothing failure.

---

## 6. Life domains

The system treats life as multiple competing domains.

Example domains:

- career;
- current job;
- learning;
- projects;
- finances;
- health;
- relationships;
- household;
- hobbies;
- gaming;
- media;
- social;
- recovery.

The planner solves a constrained allocation problem instead of allocating all available time to the highest-value professional goal.

---

## 7. Intentional leisure

A central product distinction:

> Entertainment is not automatically procrastination.

The system uses schedule + context + user intent.

Examples:

### Valid leisure

```text
20:00–22:00
Gaming block
Cyberpunk running
```

Result:

```text
No intervention.
```

### Likely avoidance

```text
14:00–15:30
Approved portfolio work block

14:07
User opens TikTok
```

Result:

```text
Possible intervention.
```

The same application can therefore be either aligned or misaligned depending on context.

---

## 8. Intervention modes

### Mode 0 — Observe

No intervention.

Only passive measurement.

### Mode 1 — Coach

Examples:

- reminder;
- suggested next action;
- progress feedback;
- replanning suggestion.

### Mode 2 — Guardrail

Adds intentional friction.

Examples:

- "You planned 45 minutes of portfolio work. Continue to TikTok?"
- 10-second delay;
- require selecting a reason;
- offer task-start shortcut.

### Mode 3 — Contract

Uses stronger pre-authorized constraints.

Examples:

- temporarily block selected applications;
- require finishing an agreed prerequisite;
- notify an accountability partner;
- consume a limited override token.

This mode must be deliberately enabled by the user.

---

## 9. Intervention ladder

The product should escalate gradually:

```text
No action
↓
Ambient cue
↓
Reminder
↓
User's own "why"
↓
Tiny next action
↓
Friction
↓
Temporary restriction
↓
Accountability escalation
```

The system should avoid repeatedly using the same ineffective action.

---

## 10. Context model

The AI should estimate at least:

### Vulnerability

How likely is the user to move away from their approved goal?

Examples:

- repeated distracting app switching;
- avoidance immediately before a difficult task;
- late-night scrolling;
- previously known failure pattern.

### Opportunity

Is this a good moment to perform a useful behavior?

Examples:

- free calendar slot;
- user already at computer;
- required project files are open;
- short task fits available time.

### Receptivity

Will the user realistically respond?

Examples:

- not in a meeting;
- not driving;
- not sleeping;
- not already in planned leisure;
- not receiving excessive prompts.

A simplified decision model:

```text
intervene =
    off_plan
    AND useful_action_exists
    AND receptivity > threshold
    AND notification_budget_available
```

---

## 11. Failure diagnosis

When an action is missed, classify likely cause:

- unrealistic workload;
- task too large;
- task unclear;
- missing dependency;
- schedule collision;
- fatigue;
- changed priority;
- deliberate rescheduling;
- avoidance;
- external event.

Different causes require different responses.

Example:

```text
Fatigue
→ reduce workload / recovery

Task too large
→ decompose

Priority changed
→ replan roadmap

Avoidance
→ stronger commitment device
```

---

## 12. Human accountability

Optional roles:

### Reviewer

Approves or comments on the initial roadmap.

### Witness

Sees lightweight summaries.

### Accountability partner

Receives selected exceptions or weekly reports.

### Coach / mentor

Can propose changes but cannot silently gain access to private raw telemetry.

Default sharing should be summaries, not raw activity streams.

---

## 13. Daily UX

The primary UI should be extremely small.

Example:

```text
TODAY

1. Finish portfolio landing page — 60 min
2. Send 15 targeted applications — 45 min
3. Polish agent demo — 40 min

Protected:
19:00–21:00 gaming
22:30 wind-down
```

The system should hide large backlogs unless requested.

---

## 14. Weekly review

Weekly review should contain:

- commitments made;
- commitments completed;
- actual time allocation;
- protected leisure respected;
- recurring blockers;
- ignored interventions;
- effective interventions;
- roadmap drift;
- proposed plan changes.

The AI should explicitly explain:

> what changed and why.

---

## 15. Long-term behavior

Success is not measured by permanent dependence on the product.

For stable habits:

```text
intervention frequency ↓
monitoring granularity ↓
user autonomy ↑
```

The ideal trajectory is:

```text
external support
→ assisted self-regulation
→ mostly autonomous behavior
```
