# Submission Metadata — Title & Description

## Title (pick one)

### Option A (Recommended — punchy, specific)
**Fair Call Agent: From "Fair Enough" to "Fair for Everyone"**

### Option B (descriptive)
**Fair Call Agent: Natural Language Constraints on Shift Scheduling**

### Option C (competitive angle)
**Fair Call Agent: 45-Point Constraint Improvement on a Production Scheduler**

---

## Description (for submission form — ~300 words)

**Fair Call Agent** is an agentic constraint-reasoning layer built on top of Fair Call Pro — a production shift scheduling app used by clinics, security firms, and call centers.

### The Problem
Fair Call Pro's deterministic LRU (Least Recently Used) scheduler distributes shifts evenly across staff. It works great when everyone is interchangeable and has no personal constraints. But real managers need to handle: _"Ada needs time off for her wedding," "Chidi can't work weekends," "Kemi only does mornings."_ The baseline scheduler ignores all of these — it produces mathematically fair schedules that are practically unusable.

### Our Agent Solution
We built a three-agent system that sits on top of the LRU scheduler:

1. **Constraint Parser** — Converts natural language instructions into 14 types of structured constraints (time-off, availability, shift preferences, inter-staff conflicts, workload limits) using pattern matching — zero LLM calls, zero external dependencies.
2. **Constraint-Aware Scheduler** — Wraps the LRU algorithm with hard-constraint filtering and soft-constraint scoring. It pre-pins specific shifts, filters ineligible staff, scores soft preferences, and gracefully degrades when understaffed.
3. **Schedule Explainer** — Analyzes the output for fairness (Gini-like score), constraint compliance, anomalies, and generates actionable insights including a "hot take" from the failure analysis.

### Measured Improvement
Across 12 realistic evaluation cases:

| Metric | Baseline | Agent | Improvement |
|---|---|---|---|
| Coverage | 100% | 100% | — |
| Fairness | 95.8/100 | 95.6/100 | -0.2 |
| **Constraint Satisfaction** | **55%** | **100%** | **+45 points** |

### Hot Take
> Back-to-back violations increase slightly (+3) when honoring time-off constraints in understaffed teams — because removing one person forces others to work consecutive days. Constraint satisfaction and individual workload smoothness are sometimes at odds. The agent's job isn't to eliminate all violations but to make transparent, principled trade-offs that the baseline can't even consider.

### Tech Stack
TypeScript, date-fns, pure pattern-matching (no LLM API calls). Built on [Fair Call Pro](https://github.com/veelawrence07-ui/fair-call-pro).

---

## Short Description (if character-limited to ~150 chars)

An agentic constraint-reasoning layer that improves shift scheduling constraint satisfaction from 55% to 100% — parsing natural language manager instructions into fair schedules.
