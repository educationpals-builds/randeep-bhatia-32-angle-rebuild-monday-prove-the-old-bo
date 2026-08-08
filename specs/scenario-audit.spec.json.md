{
  "spec_id": "trick-task-board-audit-spec",
  "product": "Trick-task board",
  "worked_example": "32-angle rebuild Monday — prove the old bot first.",
  "specimen": {
    "description": "Support bot for 32-angle rebuild Monday",
    "stakes": "Six weeks of Marisol's money into a rebuild that plateaus — and the failure will read as 'it just stopped improving', which nobody traces back to Monday",
    "usage_reality": "18,000 tickets a week, 62-word average, quoted reply chains, customers writing 'it broke again after you fixed it' with the 'it' far up the thread",
    "standard_line": "Each duty on its own line with the right party."
  },
  "sampling": {
    "source": "Named dump from the support desk.",
    "volume": "18,000 tickets a week",
    "characteristics": "62-word average, quoted reply chains, customers writing 'it broke again after you fixed it' with the 'it' far up the thread"
  },
  "rerun_triggers": {
    "change_triggers": [
      "policy/FAQ change",
      "tool wiring change"
    ],
    "calendar_floor": "biweekly",
    "rule": "Re-run on policy/FAQ or tool wiring change + biweekly floor."
  },
  "owner_roles": {
    "board_runner": "QA lead or designated bot owner",
    "leftover_owner": "Named role must own any failure that ships"
  },
  "tasks": [
    {
      "id": "p1_stale_world",
      "name": "Stale world",
      "description": "Bot quotes outdated policy when customer asks about recent changes",
      "example_input": "Shopper asks: 'What's the return window after the March policy change?' Bot quotes the pre-March 30-day FAQ.",
      "pass_line": "Bot cites current policy version with effective date",
      "verdict": "fail"
    },
    {
      "id": "p2_edge_account",
      "name": "Edge account",
      "description": "Bot handles account types absent from help-center examples",
      "example_input": "Legacy wholesale buyer: 'We're on the 2019 partner plan — can I still cancel after label print?' Plan type absent from help-center examples.",
      "pass_line": "Bot escalates or names the plan type it cannot resolve",
      "verdict": "blocked"
    },
    {
      "id": "p3_assumption_violator",
      "name": "Assumption violator",
      "description": "Input violates unstated assumptions the bot relies on",
      "example_input": "Landlord shall replace the HVAC provided that Tenant vacates.",
      "pass_line": "Bot flags when conditional structure breaks expected pattern",
      "verdict": "fail"
    },
    {
      "id": "p4_plausible_wrong",
      "name": "Plausible wrong",
      "description": "Bot produces confident but incorrect output",
      "example_input": "Tenant shall pay utilities provided that Landlord itemizes each charge.",
      "pass_line": "Bot output matches ground-truth duty assignment",
      "verdict": "fail"
    },
    {
      "id": "p5_volume_burst",
      "name": "Volume burst",
      "description": "Bot behavior under 18,000 tickets/week load with quoted reply chains",
      "pass_line": "Response quality does not degrade under volume",
      "verdict": "blocked"
    },
    {
      "id": "p6_silent_drift",
      "name": "Silent drift",
      "description": "Bot output changes without visible trigger",
      "pass_line": "Same input produces same output across runs, or drift is logged",
      "verdict": "blocked"
    },
    {
      "id": "p7_your_own",
      "name": "Churn sensing",
      "description": "It senses when a customer will churn.",
      "pass_line": "Churn prediction maps to observable field, not mind-reading verb",
      "verdict": "fail"
    },
    {
      "id": "p8_ablation",
      "name": "Ablation",
      "description": "Top crack: ablation — does removing a component change output?",
      "pass_line": "Each component's contribution is measurable",
      "verdict": "pending"
    }
  ],
  "defense_settings": {
    "name_source": {
      "label": "Name the source, or score zero",
      "explain": "No quoted customer line → no route.",
      "value": "off"
    },
    "split_bundles": {
      "label": "Split bundles before scoring",
      "explain": "Two problems → two tickets.",
      "value": "on"
    },
    "rewrite_mind_read": {
      "label": "Rewrite mind-reading verbs",
      "explain": ""Senses" / "understands" must become a real field.",
      "value": "off"
    }
  },
  "gate": {
    "block_threshold": 2,
    "rule": "BLOCKS at the number. Leftovers need an owner.",
    "leftover_requirement": "Any failure that ships must have a named owner"
  },
  "attach_rule": {
    "description": "No quoted customer line → no route",
    "enforcement": "If defense 'name_source' is on, any task without a quoted source line scores zero"
  },
  "board_aim": "Probe silent-drift first — divergence blocks ship",
  "top_crack": "ablation",
  "opposing_ruling": "Shift the gate toward what the opposing case proved",
  "sample_messages": [
    "Landlord shall replace the HVAC provided that Tenant vacates.",
    "Tenant shall pay utilities provided that Landlord itemizes each charge."
  ]
}