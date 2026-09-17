# System Architecture

## 1. High-level architecture

```text
                        ┌─────────────────────┐
                        │      User Goals     │
                        └─────────┬───────────┘
                                  │
                                  ▼
                        ┌─────────────────────┐
                        │ Goal Contract Layer │
                        └─────────┬───────────┘
                                  │
                                  ▼
                        ┌─────────────────────┐
                        │ Roadmap / Planner   │
                        └─────────┬───────────┘
                                  │
                     ┌────────────┴────────────┐
                     │                         │
                     ▼                         ▼
            ┌────────────────┐       ┌───────────────────┐
            │ Calendar/Tasks │       │ Constraint Engine │
            └───────┬────────┘       └─────────┬─────────┘
                    │                          │
                    └────────────┬─────────────┘
                                 ▼
                       ┌─────────────────────┐
                       │ Current Plan State  │
                       └─────────┬───────────┘
                                 │
        ┌────────────────────────┼────────────────────────┐
        │                        │                        │
        ▼                        ▼                        ▼
┌───────────────┐       ┌───────────────┐       ┌────────────────┐
│ Desktop Agent │       │ Mobile Agent  │       │ Wearable/Other │
└───────┬───────┘       └───────┬───────┘       └───────┬────────┘
        │                        │                       │
        └────────────────────────┼───────────────────────┘
                                 ▼
                     ┌────────────────────────┐
                     │ Context / Event Stream │
                     └───────────┬────────────┘
                                 ▼
                     ┌────────────────────────┐
                     │ Behavioral State Model │
                     └───────────┬────────────┘
                                 ▼
                     ┌────────────────────────┐
                     │ Intervention Engine    │
                     └───────────┬────────────┘
                                 ▼
                     ┌────────────────────────┐
                     │ Policy / Safety Gate   │
                     └───────────┬────────────┘
                                 ▼
                     ┌────────────────────────┐
                     │ Allowed Action         │
                     └───────────┬────────────┘
                                 ▼
                     ┌────────────────────────┐
                     │ Outcome + Learning     │
                     └────────────────────────┘
```

---

# 2. Event model

Raw events should be normalized before entering the reasoning layer.

Example:

```json
{
  "timestamp": "2026-09-17T14:07:00+02:00",
  "device": "desktop",
  "event_type": "application_focus",
  "application": "firefox",
  "category": "entertainment",
  "confidence": 0.88,
  "content": null
}
```

Whenever possible:

```text
collect category
instead of content.
```

Example:

```text
Good:
"browser category = entertainment"

More sensitive:
"full browsing history"

Very sensitive:
"continuous screen capture"
```

Use the least invasive signal that solves the problem.

---

# 3. Plan state

The planner maintains:

```yaml
current_block:
  type: goal_work
  goal_id: job_search
  action_id: targeted_applications
  start: 14:00
  end: 15:00

allowed_context:
  categories:
    - work
    - communication
    - research

protected_interruptions:
  - incoming_call
  - calendar_event

intervention_policy:
  mode: guardrail
```

---

# 4. Behavioral state

The system should maintain probabilities rather than absolute labels.

Example:

```json
{
  "aligned": 0.19,
  "deliberate_break": 0.13,
  "avoidance": 0.61,
  "unexpected_obligation": 0.07
}
```

The agent should not tell the user:

> "You are procrastinating."

unless confidence and evidence justify it.

Prefer:

> "This looks different from the block you planned. Continue, take a deliberate break, or return to the task?"

---

# 5. Intervention decision

Example pseudo-policy:

```python
if planned_leisure:
    do_nothing()

elif user_busy_or_unreceptive:
    delay()

elif short_deviation:
    observe()

elif recurring_deviation and mode == "coach":
    send_nudge()

elif recurring_deviation and mode == "guardrail":
    add_friction()

elif recurring_deviation and mode == "contract":
    request_policy_action()
```

The LLM recommends an intervention.

A deterministic policy engine decides whether that intervention is permitted.

---

# 6. Planner

Inputs:

- approved goals;
- milestone deadlines;
- task estimates;
- calendar;
- work schedule;
- protected leisure;
- rest constraints;
- dependency graph;
- actual historical completion rate.

Outputs:

- daily plan;
- weekly plan;
- slack / buffer;
- fallback actions.

Important:

Do not schedule 100% of nominal available time.

The planner should maintain uncertainty buffer.

---

# 7. Replanning

Replanning operates on multiple time scales.

### Real-time

Move or shrink one action.

### Daily

Rebalance unfinished tasks.

### Weekly

Change milestones or workload.

### Strategic

Change the roadmap itself.

Strategic changes should require stronger user approval than moving a task by 30 minutes.

---

# 8. Intervention personalization

Maintain per-user statistics:

```yaml
intervention:
  subtle_notification:
    shown: 31
    successful: 7

  why_reminder:
    shown: 14
    successful: 9

  ten_minute_start:
    shown: 18
    successful: 13

  hard_block:
    shown: 3
    override_attempts: 3
```

The system can learn that:

```text
10-minute starter action
>
generic reminder
```

for this user.

---

# 9. Memory layers

### Goal memory

Why the goal exists.

### Plan memory

Current roadmap and commitments.

### Behavioral memory

Observed patterns.

### Intervention memory

What worked and failed.

### Preference memory

User-approved interaction preferences.

### Sensitive raw telemetry

Separate storage with stricter retention rules.

The LLM should normally reason over summarized state rather than unlimited raw historical telemetry.

---

# 10. Device architecture

## Desktop

Possible signals:

- active app;
- window category;
- idle time;
- browser domain category;
- focus session;
- calendar;
- selected file/project context.

## Phone

Possible signals:

- screen time;
- foreground app category;
- notifications;
- activity state;
- calendar;
- sleep mode.

## Wearables

Optional:

- sleep;
- steps;
- activity;
- general recovery indicators.

Avoid interpreting health signals beyond what is justified by the device and user permissions.

---

# 11. Local-first processing

Preferred model:

```text
Raw events
    ↓
On-device classifier
    ↓
Abstract behavioral events
    ↓
AI reasoning
```

instead of:

```text
Raw screen / activity
    ↓
Cloud
    ↓
LLM
```

Example:

```text
Local:
youtube.com/watch?v=...
→ entertainment_video

Cloud:
"entertainment_video, 22 min"
```

This dramatically reduces sensitive-data exposure.

---

# 12. Agent model

Separate roles:

### Planner Agent

Builds roadmap.

### Scheduler

Maps roadmap into time.

### Observer

Transforms telemetry into structured state.

### Intervention Agent

Proposes responses.

### Reviewer

Checks plan quality and conflicts.

### Policy Engine

Not an LLM.

Deterministically authorizes actions.

---

# 13. Action classes

```text
Class 0
read aggregate state

Class 1
notify user

Class 2
modify own application state

Class 3
modify calendar/task system

Class 4
apply temporary local restriction

Class 5
external communication

Class 6
irreversible or high-impact action
```

Higher classes require progressively stronger authorization.

---

# 14. Explainability

Every intervention should be explainable.

Example:

```text
Why did you interrupt me?

Because:
- you approved a 14:00–15:00 application block;
- entertainment usage continued for 18 minutes;
- this pattern preceded 4 missed blocks this week;
- Guardrail mode is enabled for this goal.
```

Avoid opaque:

```text
"AI says this is best for you."
```
