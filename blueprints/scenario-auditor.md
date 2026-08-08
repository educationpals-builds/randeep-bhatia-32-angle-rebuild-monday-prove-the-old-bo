# 32-angle rebuild Monday — prove the old bot first

One-paste spec for the **Trick-task board** conversational test kit.

---

## What this blueprint covers

A stranger describes the bot they're about to trust, pastes real messages it will face, and gets eight trick tasks run against those messages. The kit returns pass/fail verdicts, the defense setting that would flip each failure, and a go-live rule with a block number and re-run trigger.

---

## Worked example domain

**Bot under test:** Support-desk ticket router handling lease-clause splitting  
**Stakes:** Six weeks of Marisol's money into a rebuild that plateaus — and the failure will read as 'it just stopped improving', which nobody traces back to Monday  
**Usage reality:** 18,000 tickets a week, 62-word average, quoted reply chains, customers writing 'it broke again after you fixed it' with the 'it' far up the thread  
**Source:** Named dump from the support desk.

### Sample messages (verbatim)

```
Landlord shall replace the HVAC provided that Tenant vacates.
Tenant shall pay utilities provided that Landlord itemizes each charge.
```

### Standard line

Each duty on its own line with the right party.

---

## The eight trick tasks

| Task ID | Task name | Verdict | Notes |
|---------|-----------|---------|-------|
| p1_stale_world | Stale world | fail | — |
| p2_edge_account | Edge account | blocked | — |
| p3_assumption_violator | Assumption violator | fail | — |
| p4_plausible_wrong | Plausible wrong | fail | — |
| p5_volume_burst | Volume burst | blocked | — |
| p6_silent_drift | Silent drift | blocked | — |
| p7_your_own | Your own task | fail | — |
| p8_churn_sense | Custom: churn sensing | — | It senses when a customer will churn. |

### Learner probes (verbatim)

1. **Stale world:** Shopper asks: 'What's the return window after the March policy change?' Bot quotes the pre-March 30-day FAQ.
2. **Edge account:** Legacy wholesale buyer: 'We're on the 2019 partner plan — can I still cancel after label print?' Plan type absent from help-center examples.

---

## Defense settings

| Defense ID | Label | Explain | Status |
|------------|-------|---------|--------|
| name_source | Name the source, or score zero | No quoted customer line → no route. | off |
| split_bundles | Split bundles before scoring | Two problems → two tickets. | on |
| rewrite_mind_read | Rewrite mind-reading verbs | "Senses" / "understands" must become a real field. | off |

---

## Go-live rule

**Gate sentence:** BLOCKS at the number. Leftovers need an owner.  
**Block threshold:** 2 failed probes  
**Re-run trigger:** Re-run on policy/FAQ or tool wiring change + biweekly floor.

---

## Board aim

Probe silent-drift first — divergence blocks ship

**Top crack:** ablation

**Opposing ruling:** Shift the gate toward what the opposing case proved

---

## Check ratings (self-scored)

| Check | Rating |
|-------|--------|
| room | 2 |
| copies | 2 |
| unowned | 2 |
| stitch | 2 |
| ablation | 4 |

---

## How a stranger uses this kit

1. Paste a description of the bot they're about to trust
2. Describe what breaks if the parts aren't really sharing the work
3. Paste real messages the bot will face (length, volume, mess)
4. Name the source of those messages
5. State the clear bar for correct output

The kit runs all eight tasks against the pasted messages, reports pass or fail with the defense that flips each failure, and returns a go-live rule with the block number (2) and the re-run trigger (policy/FAQ or tool wiring change + biweekly floor).

---

## Output structure

- Scored findings per task (pass / fail / blocked)
- Severity assessment
- Defense setting that would flip each failure
- Go-live call with block threshold
- Tripwire for post-launch monitoring
- Re-run trigger conditions
