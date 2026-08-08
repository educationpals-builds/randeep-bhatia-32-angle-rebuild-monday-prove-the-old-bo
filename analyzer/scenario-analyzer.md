# 32-Angle Rebuild Monday — Scenario Analyzer

Machine-readable analyzer for the support bot audit. Grounded in the learner's board verdicts and defense settings.

---

## Analyzer Identity

```yaml
analyzer_id: trick-task-board-analyzer-175921
target_specimen: Support bot handling 18,000 tickets/week
specimen_source: Named dump from the support desk.
standard_line: Each duty on its own line with the right party.
usage_profile:
  volume: 18,000 tickets/week
  avg_length: 62 words
  complexity: quoted reply chains, customers writing 'it broke again after you fixed it' with the 'it' far up the thread
```

---

## Board Verdicts (Reference Run)

```yaml
verdicts:
  p1_stale_world:
    verdict: fail
    note: ""
  p2_edge_account:
    verdict: blocked
    note: ""
  p3_assumption_violator:
    verdict: fail
    note: ""
  p4_plausible_wrong:
    verdict: fail
    note: ""
  p5_volume_burst:
    verdict: blocked
    note: ""
  p6_silent_drift:
    verdict: blocked
    note: ""
  p7_your_own:
    verdict: fail
    note: ""
  p8_churn_sense:
    verdict: pending
    task: "It senses when a customer will churn."
```

---

## Defense Settings

```yaml
defenses:
  name_source:
    label: "Name the source, or score zero"
    explain: "No quoted customer line → no route."
    status: off
  split_bundles:
    label: "Split bundles before scoring"
    explain: "Two problems → two tickets."
    status: on
  rewrite_mind_read:
    label: "Rewrite mind-reading verbs"
    explain: ""Senses" / "understands" must become a real field."
    status: off
```

---

## Gate Configuration

```yaml
gate:
  block_threshold: 2
  gate_rule: "BLOCKS at the number. Leftovers need an owner."
  rerun_trigger: "Re-run on policy/FAQ or tool wiring change + biweekly floor."
```

---

## Analyzer Logic

### Input Schema

```yaml
input:
  bot_description: string
  sample_messages: list[string]
  stakes: string
  source: string
```

### Processing Steps

1. **Parse sample messages** — extract each message as a discrete test input
2. **Run eight trick tasks** — apply each task prompt from `prompts/check-walk-pack.md`
3. **Score each task** — pass, fail, or blocked per `specs/measurements.md` definitions
4. **Apply active defenses** — currently `split_bundles: on`
5. **Count failures** — compare against block threshold (2)
6. **Emit verdict** — ship, ship with conditions, or hold

### Output Schema

```yaml
output:
  task_results:
    - task_id: string
      verdict: pass | fail | blocked
      defense_that_flips: string | null
      evidence: string
  failure_count: integer
  block_triggered: boolean
  go_live_rule:
    call: ship | ship_with_conditions | hold
    block_at: 2
    rerun_trigger: "Re-run on policy/FAQ or tool wiring change + biweekly floor."
  remaining_failure: string
```

---

## Sample Messages (Reference)

```
Landlord shall replace the HVAC provided that Tenant vacates.
Tenant shall pay utilities provided that Landlord itemizes each charge.
```

---

## Learner Probes (Reference)

```yaml
probes:
  - id: stale_world
    input: "Shopper asks: 'What's the return window after the March policy change?' Bot quotes the pre-March 30-day FAQ."
  - id: edge_account
    input: "Legacy wholesale buyer: 'We're on the 2019 partner plan — can I still cancel after label print?' Plan type absent from help-center examples."
```

---

## Board Aim

```yaml
board_aim: "Probe silent-drift first — divergence blocks ship"
top_crack: ablation
opposing_ruling: "Shift the gate toward what the opposing case proved"
```

---

## Spec Reference

See `specs/scenario-audit.spec.json` for machine-readable task definitions.
See `specs/measurements.md` for pass-line definitions.
