# Security and Privacy Model

## 1. Security principle

The original concept can be summarized as:

```text
AI has full access to the laptop and phone.
```

This repository deliberately changes that to:

> **Maximum useful observability, minimum necessary authority.**

Continuous context awareness and unrestricted system authority are not the same thing.

---

# 2. Why unrestricted authority is dangerous

A general-purpose AI agent may process:

- webpages;
- emails;
- documents;
- notifications;
- chat messages;
- files.

Any of these may contain:

- malicious instructions;
- prompt injection;
- adversarial content;
- misleading data.

If the same model also has unrestricted ability to:

- execute shell commands;
- delete files;
- send messages;
- move money;
- change credentials;

then a content-level attack can become a device-level incident.

---

# 3. Least privilege

The agent receives only the capability required for the present operation.

Example:

```text
Task:
"Check whether today's focus block was completed."

Required:
read aggregated app activity
read plan

Not required:
shell root
delete files
send email
access microphone
read passwords
```

Permissions should be task-scoped.

---

# 4. Deterministic policy enforcement

LLM reasoning must not be the final authorization layer.

Architecture:

```text
LLM proposal
    ↓
Structured action request
    ↓
Deterministic policy engine
    ↓
ALLOW / DENY / REQUIRE_APPROVAL
    ↓
Executor
```

Example:

```json
{
  "action": "block_application",
  "target": "tiktok",
  "duration_minutes": 25,
  "goal_id": "portfolio",
  "reason": "approved_focus_contract"
}
```

Policy:

```text
ALLOW only if:
- Contract mode enabled;
- target app is user-approved;
- duration <= authorized maximum;
- no protected exception applies.
```

---

# 5. Privilege expansion

Any permission expansion should require explicit approval.

Example:

```text
Existing:
notifications only

Requested:
application blocking

→ requires user authorization
```

The system may automatically **reduce** its permissions.

It should not automatically increase them.

---

# 6. Sensitive action classes

Always require explicit approval for actions such as:

- purchases;
- banking;
- cryptocurrency transfer;
- credential changes;
- installing software;
- deleting personal files;
- sending public posts;
- contacting employers or other people unless specifically delegated;
- disabling security controls;
- changing system-wide permissions.

This product does not need most of these actions to achieve its core purpose.

---

# 7. Raw telemetry minimization

Preferred collection hierarchy:

```text
1. aggregate category
2. application/domain
3. metadata
4. content
5. continuous raw capture
```

Move downward only when the benefit clearly justifies the privacy cost.

Example:

For distraction detection:

```text
"Instagram foreground for 24 minutes"
```

is usually enough.

The AI does not need to read private messages.

---

# 8. Local-first sensing

Sensitive raw telemetry should be processed locally whenever possible.

Example:

```text
Raw browser history
    ↓ local classifier
category timeline
    ↓
AI service
```

Store:

```text
14:07–14:31 entertainment/social
```

instead of:

```text
every URL + page content.
```

---

# 9. Retention

Recommended retention tiers:

### Raw telemetry

Hours or days.

### Structured activity events

Weeks.

### Behavioral summaries

Longer.

### Goal history

Until user deletes it.

Users should be able to independently delete:

- raw telemetry;
- behavioral summaries;
- goal memory;
- intervention history.

---

# 10. Consent is continuous

Permissions should not be treated as:

```text
Accept once forever.
```

Users should see:

- what is currently monitored;
- why;
- current authority level;
- recent agent actions;
- sharing rules;
- revoke controls.

---

# 11. Privacy dashboard

Minimum dashboard:

```text
MONITORING

Desktop application category       ON
Browser domain category             ON
Browser page content               OFF
Phone foreground applications       ON
Location                            OFF
Microphone                          OFF
Screen capture                      OFF
Health integration                  OFF
```

And:

```text
AUTHORITY

Send notifications                  ALLOWED
Move tasks                          ALLOWED
Modify calendar                     ASK
Block approved apps                 ALLOWED
Run arbitrary shell commands        DENIED
Send messages                       DENIED
Delete files                        DENIED
```

---

# 12. Accountability partner privacy

A partner should never automatically inherit raw telemetry access.

Default report:

```text
Weekly commitment completion: 72%
Focus blocks completed: 8 / 11
Main blocker: unplanned evening screen time
```

Not:

```text
full browsing history
full screen recording
private messages
```

Sharing must be user-configured.

---

# 13. Anti-abuse design

The product must not silently become surveillance software.

Important restrictions:

- user-visible installation;
- persistent indicator when monitoring is active;
- no covert monitoring;
- no hidden remote admin mode;
- clear local uninstall / disable process;
- no monitoring of another adult without their informed consent;
- strong account authentication;
- device binding.

---

# 14. Kill switch

The user always needs an immediate way to suspend:

```text
monitoring
interventions
restrictions
```

The kill switch should not require AI approval.

---

# 15. Emergency override

Even Contract mode must have an emergency override.

To preserve commitment value, override can introduce intentional friction, for example:

```text
Hold 5 sec
→ enter reason
→ disable for 30 min
```

But the system must never trap the user out of their own device.

---

# 16. Security research direction

Relevant contemporary agent-security themes include:

- task-scoped authorization;
- least-privilege tool access;
- prompt-injection isolation;
- deterministic policy enforcement;
- short-lived authorization;
- provenance;
- auditable agent actions.

The product architecture should follow these directions rather than granting a model permanent unrestricted host privileges.
