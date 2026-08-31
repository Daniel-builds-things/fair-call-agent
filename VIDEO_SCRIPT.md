# Video Demo Script — Fair Call Agent

> micro1 Agentic Workflows Hackathon · 5-minute walkthrough
> Total runtime: ~5:00

---

## [0:00 – 1:00] Origin Story & Problem

**On screen:** Open the live demo at `https://fair-call-agent-web.vercel.app` or `fair-call-agent/` in VS Code.

**Say:**
> "I built Fair Call Pro while I was interning as a medical laboratory scientist. We had a real problem — shifts and calls needed to be distributed fairly across the team, and nobody wanted to do it manually. So I wrote a scheduler.
>
> And it worked. It was actually really effective. But it was also completely deterministic — everyone was treated as interchangeable. The moment someone said 'I need time off for my wedding' or 'I can't work weekends,' the system had no idea what to do. It produced mathematically fair schedules that were practically unusable.
>
> I also realized the problem wasn't unique to healthcare — this same scheduling challenge exists in security firms, call centers, retail, hospitality, logistics. The industry doesn't matter; the constraint problem is universal.
>
> So I decided to take it further. I built an agentic layer that can understand natural language constraints using an LLM, reason about them, and produce schedules that are fair AND practical."

**Action:** Show the project structure briefly — point out the scheduler-lib core and the web UI.

---

## [1:00 – 2:30] How It Works — The Agent Layer

**On screen:** Open `src/agents/constraint-parser.ts` and `src/agents/enhanced-scheduler.ts`.

**Say:**
> "Here's the agent system. A manager types instructions in plain English — no forms, no dropdowns, no constraint builder."

**Action:** Show example constraints:
```
"Ada needs time off from Aug 14 for 3 days"
"Chidi prefers morning shifts"
"Kemi cannot work weekends"
"Bola and Emeka should not work the same shift"
```

**Say:**
> "The **Constraint Parser** converts these into structured constraint objects using an LLM — Groq for semantic understanding, with a regex fallback if no API key is configured. It handles 14 constraint types: time-off, availability, shift preferences, inter-staff conflicts, workload limits, and more.
>
> Then the **Constraint-Aware Scheduler** wraps the original LRU algorithm. For each shift, it filters out anyone who violates a hard constraint — Ada on her time-off days, Kemi on weekends. Then it scores remaining candidates against soft constraints — Chidi gets bonus points for morning slots."

**Action:** Open `src/agents/enhanced-scheduler.ts`. Point to `findEligibleStaff` — show the hard constraint filtering and soft scoring.

---

## [2:30 – 3:30] Live Demo & Results

**On screen:** Run `npm run demo` in the terminal.

**Say:**
> "Let's run it with those constraints."

**Action:** Run `npm run demo`. Show the output — the schedule respects all constraints.

**Say:**
> "That was one case. But we evaluated across 12 realistic scenarios — weddings, understaffed emergencies, hospitals with overlapping constraints, shift preference diversity, and more."

**Action:** Run `npm run eval` in the terminal.

**Say (while results print):**
> "Here are the results across all 12 cases. Coverage stays at 100% — every shift is filled. Fairness is virtually identical. But constraint satisfaction jumps from 55% to 100%. That's a 45-point improvement. The baseline accidentally satisfies some constraints by distributing evenly, but anything requiring explicit reasoning — it completely misses."

**Action:** Point at the summary table. Let it linger.

---

## [3:30 – 4:30] Iterative Build

**On screen:** Open `CHANGELOG.md`.

**Say:**
> "I didn't get to 100% in one shot. I built it iteratively:
>
> **Iteration 1** — Natural language parser for 14 constraint types. The foundation.
>
> **Iteration 2** — Constraint-aware scheduler with hard filtering and soft scoring. Jumped from 55% to about 85%.
>
> **Iteration 3** — Preference optimization. Staff who prefer certain shifts get scored higher.
>
> **Iteration 4** — Specific shift pinning. 'Ada must work morning on August 5th' gets pre-assigned.
>
> **Iteration 5** — Schedule Explainer agent for transparency — fairness scores, constraint compliance, anomaly detection.
>
> **Iteration 6** — LLM integration with Groq. The parser now uses semantic understanding for complex constraints that regex can't handle."

**Action:** Scroll through the changelog briefly.

---

## [4:30 – 5:00] Hot Take & Close

**On screen:** Show the "Hot Take" from the evaluation report or changelog.

**Say:**
> "Here's our hot take. When we honored time-off constraints in an understaffed 4-person team, back-to-back violations actually went up slightly — from 60 to 63. Why? Because removing one person forces the remaining three to work more consecutive days.
>
> This reveals something important: constraint satisfaction and workload smoothness are sometimes at odds. The agent's job isn't to eliminate all violations — it's to make transparent, principled trade-offs that the baseline can't even consider.
>
> That's Fair Call Agent. From a deterministic tool I built in a lab, to an agentic system that works for any industry. From 'fair enough' to 'fair for everyone.'"

**Action:** End on the evaluation summary: **Constraint Satisfaction: 55% → 100% [+45]**.

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
