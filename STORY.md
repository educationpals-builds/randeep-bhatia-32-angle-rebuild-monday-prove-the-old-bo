# 32-angle rebuild Monday — prove the old bot first

I built a Trick-task board to audit the support-desk bot before Marisol's team sinks six more weeks into a rebuild. The bot handles 18,000 tickets a week, 62-word average, quoted reply chains, customers writing "it broke again after you fixed it" with the "it" far up the thread.

## The task that caught it

The board ran seven tasks. Four failed outright:

- **p1_stale_world: fail** — I sent "Shopper asks: 'What's the return window after the March policy change?' Bot quotes the pre-March 30-day FAQ." The bot returned the old policy. It did not check whether the world had changed.
- **p3_assumption_violator: fail** — The bot assumed the customer's account type matched the help-center examples. It did not.
- **p4_plausible_wrong: fail** — The bot returned a confident answer that sounded right but was not.
- **p7_your_own: fail** — I asked: "It senses when a customer will churn." The bot treated "senses" as a real capability. It cannot sense anything.

Three tasks blocked before they could run:

- **p2_edge_account: blocked** — "Legacy wholesale buyer: 'We're on the 2019 partner plan — can I still cancel after label print?' Plan type absent from help-center examples."
- **p5_volume_burst: blocked**
- **p6_silent_drift: blocked**

## The defense that fixed it

I turned on **Split bundles before scoring**: Two problems → two tickets. That defense forces the bot to separate bundled issues before it routes, so a single ticket with two complaints does not get scored as one.

## The rule it now holds

The board BLOCKS at 2 failed probes. Leftovers need an owner.

## The re-run cadence

Re-run on policy/FAQ or tool wiring change + biweekly floor.

## The ruling I made

Shift the gate toward what the opposing case proved.

## The failure still open

The bot still treats mind-reading verbs as real fields. "It senses when a customer will churn" passed through without rewriting. That defense — Rewrite mind-reading verbs — is off. Someone owns that gap on go-live day.
