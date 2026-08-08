# Trick-task board

## Stranger Verification Protocol

This file confirms that a stranger can run the kit against their own bot and receive the same discipline the builder applied.

---

### What the kit must return

When a stranger pastes their bot description, stakes, and sample messages into `/play`, the kit must:

1. **Return all eight verdicts** — one for each trick task:
   - p1_stale_world: fail
   - p2_edge_account: blocked
   - p3_assumption_violator: fail
   - p4_plausible_wrong: fail
   - p5_volume_burst: blocked
   - p6_silent_drift: blocked
   - p7_your_own: fail
   - p8 (your_trick_ask): "It senses when a customer will churn."

2. **Name a defense for every failure** — each failed task must reference one of the available defenses:
   - Name the source, or score zero — No quoted customer line → no route.
   - Split bundles before scoring — Two problems → two tickets.
   - Rewrite mind-reading verbs — "Senses" / "understands" must become a real field.

3. **Refuse to publish a go-live verdict while the block number is unmet** — the kit blocks ship when 2 or more probes fail.

---

### Verification steps

**Step 1: Open /play**

Paste a bot description with:
- What the bot does
- What breaks if the parts aren't really sharing the work
- Real inputs — length, volume, mess
- Sample messages the bot will face

**Step 2: Confirm eight verdicts appear**

The kit must return a verdict (fail, blocked, or caught) for each of the eight trick tasks. No task may be skipped.

**Step 3: Confirm defenses are named**

For every failure, the kit must name which defense setting would flip it. The builder's board has **Split bundles before scoring** turned on.

**Step 4: Confirm the block rule fires**

The go-live rule: BLOCKS at the number. Leftovers need an owner.

Block threshold: 2 failed probes.

If the stranger's bot fails 2 or more probes, the kit must refuse to publish a go-live verdict. It must not say "ship" while the block number is unmet.

**Step 5: Confirm re-run trigger is stated**

The kit must return the re-run condition: Re-run on policy/FAQ or tool wiring change + biweekly floor.

---

### Builder's worked example

The builder ran this board against a support-desk bot facing:
- 18,000 tickets a week, 62-word average, quoted reply chains, customers writing 'it broke again after you fixed it' with the 'it' far up the thread

Sample messages tested:
> Landlord shall replace the HVAC provided that Tenant vacates.
> Tenant shall pay utilities provided that Landlord itemizes each charge.

Probes used:
- Stale world: Shopper asks: 'What's the return window after the March policy change?' Bot quotes the pre-March 30-day FAQ.
- Edge account: Legacy wholesale buyer: 'We're on the 2019 partner plan — can I still cancel after label print?' Plan type absent from help-center examples.

Stakes: Six weeks of Marisol's money into a rebuild that plateaus — and the failure will read as 'it just stopped improving', which nobody traces back to Monday

Standard: Each duty on its own line with the right party.

Source: Named dump from the support desk.

---

### Pass criteria

A stranger's run passes verification when:
- [ ] All eight trick-task verdicts are returned
- [ ] Every failure names a defense
- [ ] The kit blocks ship when failed probes ≥ 2
- [ ] The re-run trigger is stated
- [ ] No go-live verdict is published while the block number is unmet
