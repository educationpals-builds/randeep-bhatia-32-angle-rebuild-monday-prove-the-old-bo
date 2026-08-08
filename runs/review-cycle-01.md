# Review Cycle 01 — 32-angle rebuild Monday support bot

**Run date:** Cycle 1 reference  
**Owner:** QA lead  
**Time cost:** 38 minutes

---

## Messages pulled

Source: Named dump from the support desk.

Sample size: 50 tickets from the 18,000 tickets/week volume (62-word average, quoted reply chains, customers writing 'it broke again after you fixed it' with the 'it' far up the thread).

Sampled messages included:

> Landlord shall replace the HVAC provided that Tenant vacates.

> Tenant shall pay utilities provided that Landlord itemizes each charge.

---

## Eight verdicts produced

| Task ID | Task | Verdict |
|---------|------|---------|
| p1_stale_world | Stale world — bot quotes outdated policy | **FAIL** |
| p2_edge_account | Edge account — legacy plan absent from examples | **BLOCKED** |
| p3_assumption_violator | Assumption violator — input breaks unstated premise | **FAIL** |
| p4_plausible_wrong | Plausible wrong — confident answer, wrong route | **FAIL** |
| p5_volume_burst | Volume burst — throughput spike degrades accuracy | **BLOCKED** |
| p6_silent_drift | Silent drift — output changes without trigger | **BLOCKED** |
| p7_your_own | Custom task: It senses when a customer will churn. | **FAIL** |
| p8_churn_sense | Churn prediction claim without observable field | **FAIL** |

---

## Caught-or-missed line

**Standard line:** Each duty on its own line with the right party.

| Outcome | Count |
|---------|-------|
| FAIL | 5 |
| BLOCKED | 3 |
| PASS | 0 |

**Failed probes:** 5  
**Block threshold:** 2

**Result:** BLOCKS at the number. Leftovers need an owner.

---

## Defense settings applied

| Defense | Setting | Effect |
|---------|---------|--------|
| Name the source, or score zero | OFF | No quoted customer line → no route. |
| Split bundles before scoring | ON | Two problems → two tickets. |
| Rewrite mind-reading verbs | OFF | "Senses" / "understands" must become a real field. |

---

## Board reading

**Top crack:** ablation  
**Board aim:** Probe silent-drift first — divergence blocks ship

**Opposing ruling:** Shift the gate toward what the opposing case proved

---

## Re-run trigger

Re-run on policy/FAQ or tool wiring change + biweekly floor.

---

## Stakes reminder

Six weeks of Marisol's money into a rebuild that plateaus — and the failure will read as 'it just stopped improving', which nobody traces back to Monday

---

## Cycle summary

This reference cycle ran 50 tickets against the eight trick tasks. With 5 failures exceeding the block threshold of 2, the board returns HOLD. The split_bundles defense was active; name_source and rewrite_mind_read were off.

Next cycle due: biweekly or on policy/FAQ/tool wiring change, whichever comes first.
