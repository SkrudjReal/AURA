# AURA

**Adaptive User Regulation Agent**

> **AI that controls your whole life for “our” goal.**

A personal AI life controller that turns goals into a roadmap, watches whether reality matches the plan, intervenes when you drift, and continuously adapts your life around what you decided matters.

AURA is a concept for a personal AI system that turns long-term goals into an adaptive roadmap, observes real-world behavior across devices, intervenes at useful moments, and continuously replans around work, health, relationships, entertainment, recovery, and changing priorities.

The core idea is not another AI to-do list. It is a **closed-loop behavioral operating system**:

```text
Goal
  ↓
Goal Contract
  ↓
Roadmap
  ↓
Daily / Weekly Plan
  ↓
Real-world sensing
  ↓
Intent & context estimation
  ↓
Just-in-time intervention
  ↓
Outcome measurement
  ↓
Personalized learning
  ↓
Automatic replanning
  ↺
```

## Product thesis

Most planning tools know what a user *intends* to do, but have weak knowledge of what the user *actually does*.

AURA connects both sides:

- goals and values;
- calendar and commitments;
- current tasks;
- computer and phone activity;
- sleep / activity / recovery signals where available;
- deliberate leisure;
- distraction patterns;
- historical response to interventions.

The system's job is **not to maximize productivity**. Its job is to maximize alignment between a user's stated intentions and actual behavior without destroying rest, entertainment, relationships, or autonomy.

## Core principles

1. **User-approved goals**
   - The AI can propose a roadmap, but the user explicitly approves it.
   - A human reviewer or accountability partner can optionally review the plan.

2. **Planned leisure is first-class**
   - Gaming, films, social media, hobbies, friends, and empty time can be legitimate scheduled activities.
   - The system distinguishes deliberate leisure from unplanned avoidance.

3. **Maximum observability, minimum authority**
   - The system may observe enough contextual signals to understand behavior.
   - The LLM itself should never receive unrestricted admin/root authority.

4. **Adaptive strictness**
   - Users choose how strongly the system is allowed to intervene.
   - Strictness can vary by goal, context, time, device, and risk.

5. **Just-in-time intervention**
   - Do not notify simply because a clock says so.
   - Intervene when the user is both off-plan and likely to be receptive.

6. **Learning instead of nagging**
   - The system learns which intervention works for each user.
   - Repeatedly ignored interventions should be adapted, not spammed.

7. **Failure becomes data**
   - Missed tasks trigger diagnosis and replanning, not automatic punishment.

8. **The AI should become less necessary**
   - As behaviors become stable, intervention frequency should decrease.

## Example

User goal:

> Find an AI automation role within 10 weeks while keeping current obligations and avoiding burnout.

The system may build:

- CV and portfolio milestones;
- daily targeted applications;
- networking blocks;
- interview practice;
- project shipping;
- sleep and recovery minimums;
- fixed leisure time.

If the user opens entertainment during scheduled leisure, nothing happens.

If the user opens it during a previously approved application block, the intervention engine may:

1. wait and observe;
2. show a subtle reminder;
3. remind the user *why* the goal matters in the user's own words;
4. offer a 10-minute starter action;
5. add friction to the distraction;
6. activate a stronger pre-authorized enforcement rule.

The user controls which levels are enabled.

## What AURA is

AURA is not intended to be another task manager or generic AI life coach. The target category is closer to an **AI Life Controller / Personal Life Operating System**: a closed-loop agent that connects intention, behavior, intervention, and replanning.

The deliberately provocative product idea is simple:

> You choose the goal when you are thinking clearly. AURA helps control the environment and daily execution required to reach it.

The system must still preserve explicit user authority, revocable permissions, planned leisure, privacy boundaries, and deterministic safety controls.

## Repository structure

```text
.
├── README.md
└── docs/
    ├── PRODUCT.md
    ├── RESEARCH.md
    ├── ARCHITECTURE.md
    ├── SECURITY.md
    └── MVP.md
```

## Status

Concept / research / architecture phase.

The recommended first validation is a desktop-first MVP rather than full cross-device surveillance.

See:

- [Product specification](docs/PRODUCT.md)
- [Research rationale](docs/RESEARCH.md)
- [System architecture](docs/ARCHITECTURE.md)
- [Security and privacy model](docs/SECURITY.md)
- [MVP and validation plan](docs/MVP.md)
