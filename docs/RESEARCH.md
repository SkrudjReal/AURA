# Research Rationale

This document records the behavioral-science and HCI ideas behind AURA.

It is not a claim that the complete proposed system has already been scientifically validated.

The product combines multiple research directions whose individual components have stronger evidence than the complete integrated concept.

---

# 1. Progress monitoring

A major foundation is the evidence that monitoring progress can improve goal attainment.

Harkin et al. conducted a meta-analysis of 138 studies with 19,951 participants examining interventions designed to increase monitoring of goal progress.

Reported findings included:

- large increases in monitoring frequency;
- a small-to-medium improvement in goal attainment;
- stronger effects in some conditions when outcomes were recorded or reported.

Reference:

> Harkin, B. et al. (2016). *Does Monitoring Goal Progress Promote Goal Attainment? A Meta-Analysis of the Experimental Evidence.* Psychological Bulletin.

Product implication:

```text
Goal setting alone is insufficient.

The system should continuously compare:
current behavior
vs.
approved target behavior.
```

However, monitoring must not become obsessive or disproportionately invasive.

---

# 2. Implementation intentions

Implementation intentions are plans of the form:

```text
IF situation X occurs,
THEN I will perform action Y.
```

Research by Gollwitzer, Sheeran, and others has repeatedly investigated these plans.

A large later meta-analysis covering hundreds of tests found implementation intentions useful across behavioral, cognitive, and affective outcomes, with contingent if–then formats often performing better than vague plans.

Product implication:

Instead of:

```text
"Study English tomorrow."
```

prefer:

```text
"If it is 19:00,
I am home,
and no meeting is scheduled,
start a 30-minute English block."
```

Implementation intentions can become executable policy objects.

---

# 3. Goal setting + feedback

Behavior-change research regularly identifies combinations involving:

- goal setting;
- action planning;
- progress feedback;
- self-monitoring;
- graded tasks;
- social support.

A 2025 CHI systematic review and meta-analysis surveyed 180 HCI papers focused on goals and behavior change and found strong research concentration around goal/planning and feedback/monitoring interventions.

Reference:

> Zhu, J. et al. (CHI 2025). *A Systematic Review and Meta-Analysis of Research on Goals for Behavior Change.*

Important design observation from that review:

Most systems still focus on relatively narrow goal domains.

The authors highlight opportunities involving:

- multiple domains;
- more intrinsically meaningful goals;
- qualitative goals;
- deeper motives;
- social goals.

This maps closely to the proposed Life OS architecture.

---

# 4. Just-in-Time Adaptive Interventions (JITAIs)

JITAIs are interventions designed to offer support at moments when a person needs it and is able to benefit from it.

A typical JITAI framework contains:

- distal outcome;
- proximal outcome;
- decision points;
- tailoring variables;
- intervention options;
- decision rules.

The key idea is not:

```text
"notify user every day at 10:00"
```

but:

```text
"decide whether intervention is useful at this moment."
```

Recent reviews describe implementations using:

- smartphone data;
- wearables;
- self-report;
- passive sensing;
- contextual variables;
- rule-based systems;
- reinforcement learning / bandit approaches.

Reference:

> Hsu, T.-C. C. et al. (2024). *Personalized interventions for behaviour change: A scoping review of just-in-time adaptive interventions.*

Product implication:

The intervention engine should estimate:

```text
vulnerability
opportunity
receptivity
```

before acting.

---

# 5. Personalization

A meta-analysis of smartphone apps and activity trackers found that interventions with personalization and messaging features were associated with better outcomes in the studied physical-activity domain.

Reference:

> Laranjo, L. et al. (2021). *Do smartphone applications and activity trackers increase physical activity in adults?*

This does not directly prove identical effects for productivity.

It does support the broader hypothesis that context-sensitive personalized digital interventions can outperform generic static feedback.

---

# 6. Self-Determination Theory (SDT)

Self-Determination Theory emphasizes three psychological needs:

- autonomy;
- competence;
- relatedness.

For this project, autonomy is especially important.

A system may technically increase compliance while still undermining the user's long-term internal motivation.

Research reviews of SDT-based interventions suggest that environments supporting autonomous motivation can improve behavioral outcomes.

References:

> Gillison, F. et al. (2019). *A meta-analysis of techniques to promote motivation for health behaviour change from a self-determination theory perspective.*

> Ntoumanis, N. et al. (2021). *A meta-analysis of self-determination theory informed intervention studies in the health domain.*

Product implication:

The AI should repeatedly connect behavior to goals the user personally values.

The system should say, conceptually:

```text
"You chose this because..."
```

rather than:

```text
"The system says you must..."
```

---

# 7. Psychological reactance

Strong restrictions can cause people to attempt to restore perceived freedom.

Digital self-control research documents the tension between:

```text
too weak
→ ignored

too strong
→ frustrating / abandoned / circumvented
```

This suggests that strictness should itself be configurable and adaptive.

Reference:

> Biedermann, D., Schneider, J., & Drachsler, H. (2021). *Digital self-control interventions for distracting media multitasking — A systematic review.*

Additional HCI work discusses autonomy-supportive alternatives to rigid enforcement.

Product implication:

Use an **intervention ladder**, not a binary allow/block model.

---

# 8. Digital self-control tools

Systematic reviews of digital self-control interventions have categorized mechanisms including:

- blocking/removing;
- self-tracking;
- goal advancement;
- rewards/punishments.

Awareness alone is often insufficient.

At the same time, lockout-only strategies can be crude because they cannot distinguish intentional and unintentional use.

This project's intended contribution is therefore:

```text
context-aware self-control
```

rather than simple blocking.

---

# 9. Digital phenotyping / passive sensing

Research has explored passive behavioral signals such as:

- device usage;
- mobility;
- movement;
- sleep proxies;
- communication metadata;
- location patterns.

These approaches demonstrate that personal devices can produce useful longitudinal behavioral signals.

However, research also repeatedly identifies:

- privacy concerns;
- consent issues;
- data security;
- inaccurate inference;
- user burden;
- risk of excessive monitoring;
- lack of generalizability.

Therefore this project should borrow the sensing architecture while avoiding unnecessary medical inference.

The system should primarily infer:

```text
activity category
context
availability
plan alignment
```

not diagnose the user.

---

# 10. Privacy and monitoring acceptability

A 2025 systematic review in *npj Digital Medicine* synthesized hundreds of studies on attitudes toward health-monitoring technologies.

It reported generally positive acceptability in many studies while also identifying recurring concerns around:

- privacy;
- misuse of data;
- monitoring burden;
- autonomy;
- errors;
- security.

Reference:

> *A systematic review on patient and public attitudes toward health monitoring technologies across countries* (npj Digital Medicine, 2025).

Product implication:

Privacy cannot be a settings page added later.

It must shape the architecture.

---

# 11. Research gap

The strongest research gap relevant to this concept is the integration of:

```text
multi-domain goals
+
passive context sensing
+
goal alignment
+
adaptive intervention
+
user-selected enforcement
+
automatic replanning
```

into one general-purpose personal system.

Individual components exist.

The combined Life OS hypothesis still needs experimental validation.

---

# 12. Main hypotheses to test

## H1 — Adherence

Users with adaptive intervention will complete a higher percentage of self-approved commitments than users with planning alone.

## H2 — Context awareness

Context-aware interventions will generate fewer ignored prompts than fixed-time reminders.

## H3 — Adaptive enforcement

User-selected adaptive strictness will outperform either:

- reminder-only;
- permanent hard blocking.

## H4 — Intentional leisure

Explicitly protecting leisure will reduce perceived intrusion and improve long-term retention.

## H5 — Replanning

Failure diagnosis + automatic replanning will reduce abandonment following missed tasks.

## H6 — Autonomy

Interventions that remind users of their own stated motivation will produce lower reactance than command-style interventions.

---

# 13. Research design suggestion

A meaningful MVP experiment could compare:

### Group A

Roadmap + calendar.

### Group B

Roadmap + fixed reminders.

### Group C

Roadmap + context-sensitive intervention.

### Group D

Roadmap + context-sensitive intervention + adaptive guardrails.

Primary outcome:

```text
% of self-approved commitments completed
```

Secondary outcomes:

- override rate;
- intervention ignore rate;
- prompt count;
- perceived autonomy;
- irritation;
- retention;
- planned leisure completion;
- workload;
- plan changes;
- subjective usefulness.

Longitudinal measurement matters more than a one-day usability study.

---

# 14. Product claim discipline

Do not market unsupported claims such as:

```text
"AI increases productivity by 300%."
```

Even where implementation-intention research reports large effects, those results depend on population, outcome, study design, and context.

The product should distinguish:

```text
research-supported mechanism
```

from:

```text
validated end-to-end product outcome
```
