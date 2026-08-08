# Trick-task board

A test kit that runs eight trick tasks against any bot you're about to trust—and returns a go-live rule with a block number and a re-run trigger.

---

## What this board does

You describe the bot, who gets hurt when it quietly gets things wrong, and paste a few real messages it will face. The kit runs eight tasks against those messages, reports pass or fail with the defense that flips each failure, and returns a go-live rule.

---

## Worked example: support-desk bot

**Stakes:** Six weeks of Marisol's money into a rebuild that plateaus — and the failure will read as 'it just stopped improving', which nobody traces back to Monday

**Usage reality:** 18,000 tickets a week, 62-word average, quoted reply chains, customers writing 'it broke again after you fixed it' with the 'it' far up the thread

**Standard line:** Each duty on its own line with the right party.

**Sample messages:**
```
Landlord shall replace the HVAC provided that Tenant vacates.
Tenant shall pay utilities provided that Landlord itemizes each charge.
```

**Source:** Named dump from the support desk.

---

## Board verdict

| Task | Verdict |
|------|---------|
| p1_stale_world | fail |
| p2_edge_account | blocked |
| p3_assumption_violator | fail |
| p4_plausible_wrong | fail |
| p5_volume_burst | blocked |
| p6_silent_drift | blocked |
| p7_your_own | fail |

**Board aim:** Probe silent-drift first — divergence blocks ship

**Top crack:** ablation

---

## Defenses

| Defense | Status | Explanation |
|---------|--------|-------------|
| Name the source, or score zero | off | No quoted customer line → no route. |
| Split bundles before scoring | on | Two problems → two tickets. |
| Rewrite mind-reading verbs | off | "Senses" / "understands" must become a real field. |

---

## Go-live rule

**Gate:** BLOCKS at the number. Leftovers need an owner.

**Block at:** 2 failed probes

**Re-run trigger:** Re-run on policy/FAQ or tool wiring change + biweekly floor.

---

## Your trick task

It senses when a customer will churn.

---

## One-paste rebuild block

Paste this into the kit to rebuild the board from scratch:

```
Bot: support-desk bot
Stakes: Six weeks of Marisol's money into a rebuild that plateaus — and the failure will read as 'it just stopped improving', which nobody traces back to Monday
Usage: 18,000 tickets a week, 62-word average, quoted reply chains, customers writing 'it broke again after you fixed it' with the 'it' far up the thread
Standard: Each duty on its own line with the right party.
Messages:
Landlord shall replace the HVAC provided that Tenant vacates.
Tenant shall pay utilities provided that Landlord itemizes each charge.
Source: Named dump from the support desk.
```

---

## For strangers

A stranger describes the bot they're about to trust—what it does, who gets hurt when it quietly gets things wrong, and a few real messages it will face. The kit runs the eight tasks against those messages, reports pass or fail with the defense that flips each failure, and returns a go-live rule with a block number and a re-run trigger.

Every example is instantiated from the builder's own bot—never leave a pack sample in the shipped files.

---

## Files in this repo

- **charter.md** — Full run: eight verdicts, defenses, board reading, go-live rule, remaining failure
- **METHOD.md** — The five principles behind the board
- **VERIFY.md** — Stranger verification instructions
- **STORY.md** — Builder's first-person story

<!-- educationpals-build-verified -->
