# Reproduction Guide — Fair Call Agent

> micro1 Agentic Workflows Hackathon
> This guide walks you through running the entire evaluation suite from a clean environment.

---

## Prerequisites

| Requirement | Version | Notes |
|---|---|---|
| **Node.js** | v20+ (v22 tested) | `node --version` |
| **npm** | v10+ | `npm --version` |
| **OS** | macOS / Linux / WSL | Any Unix-like environment |
| **API Keys** | None | Zero external dependencies |

The entire project runs locally with no API keys, no Supabase, no cloud services.

---

## Step 1: Clone the Repository

```bash
git clone https://github.com/veelawrence07-ui/fair-call-agent.git
cd fair-call-agent
```

---

## Step 2: Install Dependencies

```bash
npm install
```

This installs:
- `date-fns` (v3.6.0) — date manipulation
- `tsx` (v4.19.0) — TypeScript execution
- `typescript` (v5.4.0) — type checking
- `@types/node` (v22.0.0) — Node.js type definitions

Expected output: ~3 packages, ~10 seconds.

---

## Step 3: Run the Quick Demo

```bash
npm run demo
```

This runs a single end-to-end execution:
1. Defines 8 staff members and the month of August 2025
2. Parses 3 natural language constraints
3. Runs both baseline and agent schedulers
4. Prints a side-by-side comparison
5. Generates an explanation of the agent's output

Expected duration: ~3 seconds.

---

## Step 4: Run the Full Evaluation (12 Cases)

```bash
npm run eval
```

This is the **primary evaluation command**. It:
1. Loads all 12 evaluation cases (realistic scheduling scenarios)
2. For each case, runs **both** the baseline LRU scheduler and the agentic constraint-aware scheduler
3. Measures coverage, fairness, and constraint satisfaction for each
4. Prints a summary table with aggregate results

**Expected results:**

```
========================================
  Fair Call Agent — Evaluation Summary
========================================

Cases:    12
Coverage: 100% (baseline) → 100% (agent)
Fairness: 95.8/100 (baseline) → 95.6/100 (agent)
Constraint Satisfaction: 55% (baseline) → 100% (agent) [+45 points]

Per-case breakdown:
  Case  1 (Basic 8-Staff Clinic):        ✓ Constraint satisfaction 100%
  Case  2 (Wedding Conflict):            ✓ Constraint satisfaction 100%
  Case  3 (Weekend Availability):        ✓ Constraint satisfaction 100%
  Case  4 (Night-to-Morning):            ✓ Constraint satisfaction 100%
  Case  5 (Max Shift Cap):               ✓ Constraint satisfaction 100%
  Case  6 (Pair Apart):                  ✓ Constraint satisfaction 100%
  Case  7 (Multi-Constraint Hospital):   ✓ Constraint satisfaction 100%
  Case  8 (Understaffed Emergency):      ✓ Constraint satisfaction 100%
  Case  9 (Shift Preference Diversity):  ✓ Constraint satisfaction 100%
  Case 10 (No Back-to-Back Policy):      ✓ Constraint satisfaction 100%
  Case 11 (Holiday Month):               ✓ Constraint satisfaction 100%
  Case 12 (Specific Shift Assignment):   ✓ Constraint satisfaction 100%
```

Expected duration: ~5 seconds.

---

## Step 5: Generate HTML Evaluation Report

```bash
npm run eval:html
```

This produces a visual HTML report at `eval-report/index.html` with:
- Side-by-side baseline vs agent charts
- Per-case constraint breakdowns
- Fairness distribution graphs
- Hot take / failure analysis

Open `eval-report/index.html` in any browser.

---

## Step 6: Run Constraint Tests

```bash
npm run test
```

Runs unit-level tests on the constraint parser to verify all 14 constraint types are correctly identified from natural language.

---

## Project Structure

```
fair-call-agent/
├── src/
│   ├── lib/
│   │   └── baseline-scheduler.ts   # Original LRU algorithm (baseline)
│   ├── agents/
│   │   ├── constraint-parser.ts     # NL → structured constraints
│   │   ├── enhanced-scheduler.ts    # Constraint-aware scheduler
│   │   └── schedule-explainer.ts    # Analysis + insights
│   ├── eval/
│   │   ├── cases.ts                 # 12 evaluation cases
│   │   └── evaluate.ts              # Benchmark runner
│   ├── types.ts                     # Shared types
│   └── index.ts                     # Demo entry point
├── scripts/
│   └── generate_eval_html.ts        # HTML report generator
├── eval-report/
│   └── index.html                   # Generated report
├── CHANGELOG.md                     # 5 improvement iterations
├── REPRODUCE.md                     # This file
├── package.json
└── tsconfig.json
```

---

## Cost & Runtime

| Metric | Value |
|---|---|
| API calls | 0 |
| External services | 0 |
| LLM cost | $0.00 |
| Total runtime (full eval) | ~5 seconds |
| Memory usage | <50 MB |
| Node.js version | v22 (v20+ compatible) |

---

## Troubleshooting

| Issue | Fix |
|---|---|
| `node: command not found` | Install Node.js from https://nodejs.org |
| `tsx: not found` | Run `npm install` first |
| TypeScript errors | Run `npm run build` to check compilation |
| Evaluation fails | Ensure you're in the `fair-call-agent/` root directory |

---

## What to Show Judges

For the hackathon evaluation, the most important command is:

```bash
npm run eval
```

This single command demonstrates the **measured improvement** — the core scoring criterion. It runs both baseline and agent across 12 cases and prints the +45 point constraint satisfaction improvement.
