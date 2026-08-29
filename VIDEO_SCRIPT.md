# Video Demo Script — Fair Call Agent

> micro1 Agentic Workflows Hackathon · 5-minute walkthrough
> Total runtime: ~5:00

---

## [0:00 – 0:30] Problem & Baseline

**On screen:** Open `fair-call-agent/` in VS Code. Show the project structure briefly.

**Say:**
> "Shift scheduling sounds simple — just distribute shifts fairly across your team, right? That's exactly what Fair Call Pro does with its LRU algorithm. And it works great... until someone says 'I need time off for my wedding' or 'I can't work weekends.'
>
> The baseline scheduler has no idea how to handle those constraints. It produces mathematically fair schedules that are practically unusable.
>
> We built an agent layer that changes that."

**Action:** Open `src/lib/baseline-scheduler.ts`. Scroll to show it's a clean, well-structured algorithm. Point out it has no concept of constraints.

---

## [0:30 – 2:00] One Realistic Execution

**On screen:** Open `src/index.ts` (the demo entry point).

**Say:**
> "Here's how it works. A manager types natural language instructions — no forms, no dropdowns, no constraint builder UI."

**Action:** Show the demo constraints in the code:
```
"Ada needs time off from Aug 14 for 3 days"
"Chidi prefers morning shifts"
"Kemi cannot work weekends"
```

**Say:**
> "The Constraint Parser converts these into structured constraint objects — time-off, preference, and availability. No LLM API calls, just pattern matching."

**Action:** Open `src/agents/constraint-parser.ts`. Briefly show the regex patterns.

**Say:**
> "Then the Enhanced Scheduler wraps the original LRU algorithm. For each shift slot, it first filters out anyone who would violate a hard constraint — like Ada on her time-off days, or Kemi on weekends. Then it scores remaining candidates with soft constraints — Chidi gets a bonus for morning slots."

**Action:** Open `src/agents/enhanced-scheduler.ts`. Show the `findEligibleStaff` function — point out the hard constraint filtering and soft scoring.

**Say:**
> "Let's run it."

**Action:** Run `npm run demo` in the terminal. Show the output appearing.

---

## [2:00 – 3:30] Comparison Results

**On screen:** Terminal showing the demo output. Then switch to running the full evaluation.

**Say:**
> "That was one case. But we evaluated across 12 realistic scenarios — weddings, understaffed emergencies, hospitals with multiple overlapping constraints, shift preference diversity, and more."

**Action:** Run `npm run eval` in the terminal.

**Say (while results print):**
> "Here are the results. Coverage stays at 100% — every shift is filled. Fairness is virtually identical at 95.6 versus 95.8. But constraint satisfaction — that's the key metric — jumps from 55% to 100%. That's a 45-point improvement.
>
> The baseline accidentally satisfies some constraints just because the LRU algorithm distributes evenly. But anything requiring explicit reasoning — time-off requests, weekend unavailability, shift preferences — the baseline completely misses."

**Action:** Point at the summary table on screen. Let it linger for a moment.

---

## [3:30 – 4:30] Changelog Highlights

**On screen:** Open `CHANGELOG.md`. Scroll through the 5 iterations.

**Say:**
> "We didn't get to 100% in one shot. We built it iteratively, measuring each step:
>
> **Iteration 1** — We added a natural language parser supporting 14 constraint types. This was the foundation.
>
> **Iteration 2** — We built the constraint-aware scheduling engine with hard constraint filtering and soft scoring. This alone jumped us from 55% to about 85%.
>
> **Iteration 3** — We added preference optimization. Staff who prefer certain shifts get scored higher. This brought preference satisfaction from zero to 100%.
>
> **Iteration 4** — We added specific shift pinning. When a manager says 'Ada must work morning on August 5th,' that gets pre-assigned before the main loop.
>
> **Iteration 5** — We built the Schedule Explainer — a separate agent that analyzes the output for fairness, constraint compliance, and anomalies. This gives managers transparency into why the schedule looks the way it does."

**Action:** Briefly scroll through each iteration in the changelog.

---

## [4:30 – 5:00] Hot Take & Close

**On screen:** Show the "Hot Take" section from the changelog or the evaluation report.

**Say:**
> "Here's our hot take. When we honored time-off constraints in an understaffed 4-person team, back-to-back violations actually went up slightly — from 60 to 63. Why? Because removing one person forces the remaining three to work more consecutive days.
>
> This reveals something important: constraint satisfaction and individual workload smoothness are sometimes at odds. The agent's job isn't to eliminate all violations — it's to make transparent, principled trade-offs that the baseline algorithm can't even consider.
>
> That's Fair Call Agent. From 'fair enough' to 'fair for everyone.'"

**Action:** Show the final evaluation summary one more time. End on the constraint satisfaction: **55% → 100% [+45]**.

---

## Recording Tips

1. **Use VS Code** with a clean theme (Dark+ or One Dark Pro work well)
2. **Set terminal font size to 14+** so output is readable
3. **Run `npm run eval` beforehand** so you know what the output looks like
4. **Practice the timing** — read the script aloud while clicking through once before recording
5. **Use a screen recorder** like OBS, QuickTime, or Loom
6. **Speak naturally** — the script is a guide, not a teleprompter. Adjust phrasing to your style.
7. **Keep pauses short** — 5 minutes goes fast. If you're over, trim the changelog section.
8. **Mute notifications** before recording
