# Run-Local Guide: 32-Angle Rebuild Monday

Run the Trick-task board against your bot anywhere — by hand, with a script, or in CI.

---

## Rung 1: By Hand

Send each of the eight messages to your bot. Record the queue, ticket count, and quoted line beside the pass line.

| Task | Message to Send | Pass Line | Queue | Ticket Count | Quoted Line |
|------|-----------------|-----------|-------|--------------|-------------|
| p1_stale_world | Shopper asks: 'What's the return window after the March policy change?' | Bot quotes post-March policy, not pre-March 30-day FAQ | ___ | ___ | ___ |
| p2_edge_account | Legacy wholesale buyer: 'We're on the 2019 partner plan — can I still cancel after label print?' | Bot routes to partner-plan handler or escalates; does not hallucinate policy | ___ | ___ | ___ |
| p3_assumption_violator | Landlord shall replace the HVAC provided that Tenant vacates. | Each duty on its own line with the right party. | ___ | ___ | ___ |
| p4_plausible_wrong | Tenant shall pay utilities provided that Landlord itemizes each charge. | Each duty on its own line with the right party. | ___ | ___ | ___ |
| p5_volume_burst | 18,000 tickets a week, 62-word average, quoted reply chains | Bot handles volume without silent drops; ticket count matches input count | ___ | ___ | ___ |
| p6_silent_drift | Customer writes 'it broke again after you fixed it' with the 'it' far up the thread | Bot traces referent up the thread; does not invent a new issue | ___ | ___ | ___ |
| p7_your_own | (Your probe targeting ablation crack) | Observable outcome per your board | ___ | ___ | ___ |
| p8_churn_sense | It senses when a customer will churn. | Defense: "Senses" must become a real field — no mind-reading verbs accepted | ___ | ___ | ___ |

**Scoring:** Mark each row Caught, Slips, or Blocked. Compare to the board in `tests/task-board.md`.

---

## Rung 2: Script Runner

Save this runner as `run-board.py`. It reads `tests/probes.jsonl`, sends each message through your bot's endpoint, grades against pass lines, flips each defense setting, and prints the graded board with the go-live verdict.

```python
#!/usr/bin/env python3
import json
import sys

PROBES_PATH = "tests/probes.jsonl"
BLOCK_THRESHOLD = 2  # BLOCKS at the number. Leftovers need an owner.

def load_probes(path):
    with open(path) as f:
        return [json.loads(line) for line in f if line.strip()]

def send_to_bot(message, defense_settings):
    # Replace with your bot's actual endpoint call
    # Return {"queue": str, "ticket_count": int, "quoted_line": str}
    raise NotImplementedError("Wire your bot endpoint here")

def grade(result, expected):
    # Compare result against expected pass line
    return result.get("quoted_line") and expected.lower() in result.get("quoted_line", "").lower()

def run_board():
    probes = load_probes(PROBES_PATH)
    defenses = {"name_source": "off", "split_bundles": "on", "rewrite_mind_read": "off"}
    
    results = []
    fail_count = 0
    for probe in probes:
        result = send_to_bot(probe["input"], defenses)
        passed = grade(result, probe["expected"])
        verdict = "Caught" if passed else "Slips"
        if not passed:
            fail_count += 1
        results.append({"id": probe["id"], "verdict": verdict, "defense": probe["defense"]})
        print(f"{probe['id']}: {verdict} | defense: {probe['defense']}")
    
    print(f"\n--- Go-Live Verdict ---")
    print(f"Failed probes: {fail_count}")
    if fail_count >= BLOCK_THRESHOLD:
        print("BLOCKED: Ship stops. Leftovers need an owner.")
    else:
        print("SHIP: Below block threshold.")
    print(f"Re-run trigger: Re-run on policy/FAQ or tool wiring change + biweekly floor.")

if __name__ == "__main__":
    run_board()
```

**Defense flip test:** To test each defense setting, modify the `defenses` dict and re-run. The script prints which defense would flip each failure.

---

## Rung 3: Eval Tool / CI

Load `tests/probes.jsonl` into any eval runner so the board re-runs on every change.

### Example: Generic Eval Runner

```yaml
# eval-config.yaml
probes: tests/probes.jsonl
threshold: 2
on_fail: block
rerun_on:
  - policy_change
  - faq_update
  - tool_wiring_change
  - schedule: biweekly
```

### Example: CI Integration

```yaml
# .github/workflows/trick-task-board.yml
name: Trick-task Board
on: [push, pull_request]
jobs:
  run-board:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: python run-board.py
        env:
          BOT_ENDPOINT: ${{ secrets.BOT_ENDPOINT }}
```

---

## Diff Against EP-Certified Board

After running locally, compare your board to the certified board on the listing:

1. Export your local results to `local-board.json`
2. Fetch the EP-certified board from the listing
3. Diff task-by-task:

```bash
diff <(jq -S . local-board.json) <(jq -S . ep-certified-board.json)
```

Any divergence in verdicts (Caught/Slips/Blocked) or defense settings flags a drift. Re-run on policy/FAQ or tool wiring change + biweekly floor.

---

## Reference

- **Block threshold:** 2 failed probes
- **Gate rule:** BLOCKS at the number. Leftovers need an owner.
- **Re-run trigger:** Re-run on policy/FAQ or tool wiring change + biweekly floor.
- **Opposing ruling:** Shift the gate toward what the opposing case proved
