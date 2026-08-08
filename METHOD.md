# PRISM: The Five Principles Behind the Trick-Task Board

This file is the only place the framework letters appear. Every other file in this repository opens as the Trick-task board product.

---

## P — Partition the Space

Before you run a single probe, split the input space into regions that could fail differently.

A support-desk bot handling 18,000 tickets a week, 62-word average, quoted reply chains—customers writing "it broke again after you fixed it" with the "it" far up the thread—does not fail uniformly. It fails on stale policy, on edge account types, on assumption violations, on plausible-wrong answers, on volume bursts, on silent drift, and on your own trick task.

Partition first. Then each probe lands in exactly one region.

---

## R — Run in Parallel

Run probes against each partition at the same time, not in sequence.

When you run sequentially, early failures bias your attention. You fix the stale-world probe and never notice the edge-account probe was blocked. Parallel execution surfaces the full failure surface before you start patching.

---

## I — Individuate the Pattern

Each probe must target one failure pattern, not a bundle.

A probe like "Shopper asks: 'What's the return window after the March policy change?' Bot quotes the pre-March 30-day FAQ" targets stale world. A probe like "Legacy wholesale buyer: 'We're on the 2019 partner plan — can I still cancel after label print?' Plan type absent from help-center examples" targets edge account.

If a probe could fail for two reasons, split it. Two problems → two tickets.

---

## S — Stitch the Spectra

After probes return, stitch verdicts into a single board reading.

Your board shows: p1_stale_world = fail, p2_edge_account = blocked, p3_assumption_violator = fail, p4_plausible_wrong = fail, p5_volume_burst = blocked, p6_silent_drift = blocked, p7_your_own = fail.

That spectrum tells you where the bot actually breaks. A single pass/fail count hides the shape.

---

## M — Map What Each Head Sees

For every failure, map the defense that would flip it.

Your defense state:
- **Name the source, or score zero** — No quoted customer line → no route.
- **Split bundles before scoring** — Two problems → two tickets. *(enabled)*
- **Rewrite mind-reading verbs** — "Senses" / "understands" must become a real field.

When the board says "fail," the defense map says which lever to pull.

---

## The Collapse-to-Monochrome Anti-Pattern

The opposite of PRISM is collapsing everything to a single color: one probe, one verdict, one "it works" or "it doesn't."

A bot that handles "Landlord shall replace the HVAC provided that Tenant vacates" and "Tenant shall pay utilities provided that Landlord itemizes each charge" might pass a single happy-path test and still fail on stale world, edge accounts, assumption violators, plausible-wrong answers, volume bursts, silent drift, and your own trick task.

Monochrome testing hides the failure until six weeks of Marisol's money goes into a rebuild that plateaus—and the failure reads as "it just stopped improving," which nobody traces back to Monday.

PRISM keeps the spectrum visible. The board blocks at 2 failed probes. Leftovers need an owner. Re-run on policy/FAQ or tool wiring change + biweekly floor.

---

*These five letters appear only in this file. Every other file in this repository names the Trick-task board as the product and grounds examples in the builder's own bot.*
