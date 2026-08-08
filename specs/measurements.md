# Pass-Line Measurements — 32-Angle Rebuild Monday Support Bot

Observable definitions for each trick task. Every pass line names the queue, count, quoted line, and route-match rule — plus the defense setting it depends on.

---

## Environment

- **Volume**: 18,000 tickets a week, 62-word average, quoted reply chains, customers writing 'it broke again after you fixed it' with the 'it' far up the thread
- **Source**: Named dump from the support desk.
- **Standard**: Each duty on its own line with the right party.

---

## Task Pass Lines

### P1 — Stale World

| Observable | Definition |
|------------|------------|
| Queue | Ticket lands in **Escalation-Policy-Mismatch** if the bot quotes a superseded FAQ |
| Count | One ticket per policy gap cited |
| Quoted line | The pre-change FAQ sentence the bot returned must appear in the escalation note |
| Same route | Two layouts match if both cite the same FAQ article ID and the same date-range boundary |
| Defense dependency | **name_source** — if off, no quoted customer line required; if on, route fails without it |

**Example input**: Shopper asks: 'What's the return window after the March policy change?' Bot quotes the pre-March 30-day FAQ.

---

### P2 — Edge Account

| Observable | Definition |
|------------|------------|
| Queue | Ticket lands in **Manual-Review-Legacy** when account type is absent from help-center examples |
| Count | One ticket per unrecognized plan type |
| Quoted line | The customer's plan identifier (e.g., "2019 partner plan") must appear verbatim in the review note |
| Same route | Two layouts match if both flag the same plan-type string and the same missing-example gap |
| Defense dependency | **split_bundles** — if on, two problems in one message open two tickets |

**Example input**: Legacy wholesale buyer: 'We're on the 2019 partner plan — can I still cancel after label print?' Plan type absent from help-center examples.

---

### P3 — Assumption Violator

| Observable | Definition |
|------------|------------|
| Queue | Ticket lands in **Assumption-Breach** when the input violates a silent premise the bot holds |
| Count | One ticket per violated assumption |
| Quoted line | The customer sentence that breaks the assumption must be quoted in the breach note |
| Same route | Two layouts match if both identify the same assumption and the same violating clause |
| Defense dependency | **rewrite_mind_read** — if on, any "senses" / "understands" verb must become a real field before scoring |

---

### P4 — Plausible Wrong

| Observable | Definition |
|------------|------------|
| Queue | Ticket lands in **Confident-Incorrect** when the bot returns a plausible but wrong answer |
| Count | One ticket per wrong answer that reads as correct |
| Quoted line | The incorrect bot output and the customer's original question must both appear in the ticket |
| Same route | Two layouts match if both cite the same wrong answer and the same source of confusion |
| Defense dependency | **name_source** — if on, no route without a quoted customer line |

---

### P5 — Volume Burst

| Observable | Definition |
|------------|------------|
| Queue | Ticket lands in **Capacity-Overflow** when throughput exceeds the bot's tested ceiling |
| Count | One ticket per burst event that degrades response quality |
| Quoted line | The timestamp range and ticket count of the burst must appear in the overflow note |
| Same route | Two layouts match if both flag the same time window and the same degradation pattern |
| Defense dependency | **split_bundles** — if on, bundled complaints during burst open separate tickets |

---

### P6 — Silent Drift

| Observable | Definition |
|------------|------------|
| Queue | Ticket lands in **Drift-Detection** when bot behavior diverges from baseline without alert |
| Count | One ticket per drift instance detected |
| Quoted line | The baseline response and the drifted response must both appear in the detection note |
| Same route | Two layouts match if both identify the same input class and the same direction of drift |
| Defense dependency | **name_source** — if on, the original customer line that triggered drift must be quoted |

---

### P7 — Your Own (Churn Sensing)

| Observable | Definition |
|------------|------------|
| Queue | Ticket lands in **Mind-Read-Failure** when the bot claims to "sense" churn without a real field |
| Count | One ticket per churn prediction that lacks an observable basis |
| Quoted line | The bot's churn claim and the missing field must both appear in the failure note |
| Same route | Two layouts match if both cite the same prediction verb and the same absent data source |
| Defense dependency | **rewrite_mind_read** — if on, "senses when a customer will churn" must become a real field or score zero |

**Learner's task**: It senses when a customer will churn.

---

### P8 — Compound Duty Split

| Observable | Definition |
|------------|------------|
| Queue | Ticket lands in **Bundle-Split-Required** when a single message contains multiple duties |
| Count | Two tickets must open when two problems appear in one message |
| Quoted line | Each duty must appear on its own line with the right party |
| Same route | Two layouts match if both split the same compound into the same duty pairs |
| Defense dependency | **split_bundles** — if on, two problems → two tickets; if off, bundle stays merged |

**Example sentences**:
- Landlord shall replace the HVAC provided that Tenant vacates.
- Tenant shall pay utilities provided that Landlord itemizes each charge.

---

## Defense Settings Summary

| Defense | Current State | Effect on Pass Lines |
|---------|---------------|----------------------|
| name_source | off | No quoted customer line required for route |
| split_bundles | on | Two problems → two tickets |
| rewrite_mind_read | off | "Senses" / "understands" verbs allowed without field rewrite |

---

## Block Threshold

Ship stops at **2 Slips rows**.

Gate rule: BLOCKS at the number. Leftovers need an owner.

---

## Re-Run Triggers

Re-run on policy/FAQ or tool wiring change + biweekly floor.
