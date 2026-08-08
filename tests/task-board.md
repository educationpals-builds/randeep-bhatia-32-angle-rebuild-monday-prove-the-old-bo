# 32-angle rebuild Monday — prove the old bot first

## Task Board: Eight Trick Tasks

This board runs eight tasks against the support bot before the rebuild. Each task probes a specific failure mode. Verdicts: **Caught** (bot handled it), **Slips** (bot failed), **Hold** (blocked from testing).

---

### Specimen context

- **Stakes:** Six weeks of Marisol's money into a rebuild that plateaus — and the failure will read as 'it just stopped improving', which nobody traces back to Monday
- **Usage reality:** 18,000 tickets a week, 62-word average, quoted reply chains, customers writing 'it broke again after you fixed it' with the 'it' far up the thread
- **Standard line:** Each duty on its own line with the right party.
- **Source:** Named dump from the support desk.

---

## The Eight Tasks

### Task 1: Stale World (p1_stale_world)

**Message:**  
> Shopper asks: 'What's the return window after the March policy change?' Bot quotes the pre-March 30-day FAQ.

**What the bot did:** Quoted outdated FAQ — pre-March 30-day policy instead of current policy.

**Verdict:** Slips

**Defense that flips this failure:**  
- **Name the source, or score zero** — No quoted customer line → no route.

---

### Task 2: Edge Account (p2_edge_account)

**Message:**  
> Legacy wholesale buyer: 'We're on the 2019 partner plan — can I still cancel after label print?' Plan type absent from help-center examples.

**What the bot did:** Could not test — plan type absent from help-center examples.

**Verdict:** Hold

**Defense that flips this failure:**  
- **Split bundles before scoring** — Two problems → two tickets.

---

### Task 3: Assumption Violator (p3_assumption_violator)

**Message:**  
> Landlord shall replace the HVAC provided that Tenant vacates.

**What the bot did:** Assigned duty without parsing the conditional — missed that replacement depends on vacancy.

**Verdict:** Slips

**Defense that flips this failure:**  
- **Name the source, or score zero** — No quoted customer line → no route.

---

### Task 4: Plausible Wrong (p4_plausible_wrong)

**Message:**  
> Tenant shall pay utilities provided that Landlord itemizes each charge.

**What the bot did:** Routed to Tenant queue without flagging the itemization condition — plausible but incomplete.

**Verdict:** Slips

**Defense that flips this failure:**  
- **Split bundles before scoring** — Two problems → two tickets.

---

### Task 5: Volume Burst (p5_volume_burst)

**Message:**  
> Customer writes 'it broke again after you fixed it' with the 'it' far up the thread — part of a 62-word average reply chain.

**What the bot did:** Could not test at volume — blocked by queue limits.

**Verdict:** Hold

**Defense that flips this failure:**  
- **Split bundles before scoring** — Two problems → two tickets.

---

### Task 6: Silent Drift (p6_silent_drift)

**Message:**  
> Same ticket, two layouts: original support form vs. new mobile form. Bot should route identically.

**What the bot did:** Could not test — no second layout available in test environment.

**Verdict:** Hold

**Defense that flips this failure:**  
- **Rewrite mind-reading verbs** — "Senses" / "understands" must become a real field.

---

### Task 7: Learner Probe — Stale World (p7_your_own)

**Message:**  
> Shopper asks: 'What's the return window after the March policy change?' Bot quotes the pre-March 30-day FAQ.

**What the bot did:** Quoted stale FAQ — failed to surface current policy.

**Verdict:** Slips

**Defense that flips this failure:**  
- **Name the source, or score zero** — No quoted customer line → no route.

---

### Task 8: Churn Sense (p8_churn_sense)

**Message:**  
> It senses when a customer will churn.

**What the bot did:** No observable field for "senses" — mind-reading verb with no grounded signal.

**Verdict:** Slips

**Defense that flips this failure:**  
- **Rewrite mind-reading verbs** — "Senses" / "understands" must become a real field.

---

## This Run's Board

| Task ID | Task Name | Verdict | Defense Setting |
|---------|-----------|---------|-----------------|
| p1_stale_world | Stale World | Slips | Name the source, or score zero |
| p2_edge_account | Edge Account | Hold | Split bundles before scoring |
| p3_assumption_violator | Assumption Violator | Slips | Name the source, or score zero |
| p4_plausible_wrong | Plausible Wrong | Slips | Split bundles before scoring |
| p5_volume_burst | Volume Burst | Hold | Split bundles before scoring |
| p6_silent_drift | Silent Drift | Hold | Rewrite mind-reading verbs |
| p7_your_own | Learner Probe — Stale World | Slips | Name the source, or score zero |
| p8_churn_sense | Churn Sense | Slips | Rewrite mind-reading verbs |

---

## Defense Settings (Current State)

| Defense | Status | Explanation |
|---------|--------|-------------|
| Name the source, or score zero | off | No quoted customer line → no route. |
| Split bundles before scoring | on | Two problems → two tickets. |
| Rewrite mind-reading verbs | off | "Senses" / "understands" must become a real field. |

---

## Board Summary

- **Slips:** 5 tasks (p1, p3, p4, p7, p8)
- **Hold:** 3 tasks (p2, p5, p6)
- **Caught:** 0 tasks

**Board aim:** Probe silent-drift first — divergence blocks ship

**Top crack targeted:** ablation
