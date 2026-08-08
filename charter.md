# Trick-task board

## Charter: Full audit run

**Worked example domain:** 32-angle rebuild Monday — prove the old bot first.

**Bot under test:** Support-desk bot handling 18,000 tickets a week, 62-word average, quoted reply chains, customers writing 'it broke again after you fixed it' with the 'it' far up the thread.

**Stakes:** Six weeks of Marisol's money into a rebuild that plateaus — and the failure will read as 'it just stopped improving', which nobody traces back to Monday

**Standard (clear bar):** Each duty on its own line with the right party.

**Source:** Named dump from the support desk.

---

## Sample messages tested

```
Landlord shall replace the HVAC provided that Tenant vacates.
Tenant shall pay utilities provided that Landlord itemizes each charge.
```

---

## Learner probes

1. **Stale world:** Shopper asks: 'What's the return window after the March policy change?' Bot quotes the pre-March 30-day FAQ.
2. **Edge account:** Legacy wholesale buyer: 'We're on the 2019 partner plan — can I still cancel after label print?' Plan type absent from help-center examples.

---

## Board aim

Probe silent-drift first — divergence blocks ship

---

## Eight verdicts

| Task | Verdict |
|------|---------|
| p1_stale_world | **fail** |
| p2_edge_account | **blocked** |
| p3_assumption_violator | **fail** |
| p4_plausible_wrong | **fail** |
| p5_volume_burst | **blocked** |
| p6_silent_drift | **blocked** |
| p7_your_own | **fail** |
| p8_your_trick_ask | It senses when a customer will churn. |

**Summary:** 4 fail, 3 blocked, 1 custom trick task recorded.

---

## Defenses turned on

| Defense | Status | Explanation |
|---------|--------|-------------|
| Name the source, or score zero | off | No quoted customer line → no route. |
| Split bundles before scoring | **on** | Two problems → two tickets. |
| Rewrite mind-reading verbs | off | "Senses" / "understands" must become a real field. |

---

## Board reading

**Top crack:** ablation

**Opposing ruling:** Shift the gate toward what the opposing case proved

---

## Go-live rule

**Gate sentence:** BLOCKS at the number. Leftovers need an owner.

**Block at:** 2 failed probes

**Re-run trigger:** Re-run on policy/FAQ or tool wiring change + biweekly floor.

---

## Failure that remains

The board recorded four failures and three blocked tasks. With the block threshold set at 2 failed probes, ship is currently blocked. The enabled defense (Split bundles before scoring) addresses bundled-problem tickets but does not resolve stale-world, assumption-violator, plausible-wrong, or the custom trick task failures.

The custom trick task — "It senses when a customer will churn." — names a mind-reading verb that the "Rewrite mind-reading verbs" defense would address, but that defense is currently off.

Leftovers need an owner before go-live.
