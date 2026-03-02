# dialectic (compact)

Two Electric Monk subagents believe opposing positions at full conviction. Orchestrator performs structural contradiction analysis and synthesis (Aufhebung). User operates from belief-free position.

## When to Use

Use when: stress-testing an idea, genuine tension between positions, high-stakes decision with unclear tradeoffs, building a deeper mental model.
Do NOT use when: purely empirical question, one side obviously correct, user wants quick recommendation.

## Core Frameworks

- **Rao:** Artificial belief system — monks BELIEVE, not think. Anti-hedging is functional, not stylistic.
- **Hegel:** Determinate negation → synthesis cancels, preserves, elevates. NOT compromise.
- **Boyd:** Shatter positions into atoms, find cross-domain connections. New synthesis requires material from outside original domains.

## 7-Phase Flow

```
Phase 1: Elenctic Interview + Research (orchestrator + user)
  1a: Explain process, set user as co-pilot
  1b: Mode A (stress-test one idea) or Mode B (two positions in tension)
  1c: Socratic probing — hidden assumptions, deepest contradiction, domain type
  1c′: Identify belief burden (read references/belief-burdens.md) → calibrate monk roles
  1d: Ground monks — research depth is the main knob:
      Novel domain: 2-3 parallel research agents, 150-250K tokens
      Well-known: skip research, write briefing from knowledge
      Personal: deep interview IS the research (6-10 exchanges)
  1e: Write context_briefing.md — resolve output dir to ABSOLUTE path first
      Slug: lowercase, hyphens, max 40 chars, date-prefix recommended
  1f: USER CHECKPOINT — confirm framing, ask "missing companies/thinkers/evidence?"

Phase 2: Generate Monk Prompts
  Read references/monk-prompt-template.md for 7-section template
  Key: role + framing corrections + context briefing + research directives +
       argument structure + anti-hedging + length (1500-2000w R1, 1000-1500w recursive)

Phase 3: Spawn Electric Monks
  Two parallel Agent calls: subagent_type="general-purpose", run_in_background=true
  Write outputs to [OUTPUT_DIR]/monk_a_output.md, monk_b_output.md
  Decorrelation check: different evidence? different vocabularies? different assumptions?
  USER CHECKPOINT — accurate? missing evidence?

Phase 4: Determinate Negation (orchestrator only — do NOT delegate)
  Write to [OUTPUT_DIR]/determinate_negation.md
  4.0: Internal tensions — where does each position undermine itself?
  4.1: Surface contradiction (simplest form)
  4.2: Shared assumptions (same unit of analysis? same central problem?)
  4.3: Determinate negation — SPECIFIC failure → SPECIFIC missing thing (complementary)
  4.4: Hidden question neither monk asked
  4.5: Boydian decomposition — generic space, atomic components, surprising cross-connections
  4.6: Sublation criteria — what must synthesis preserve/dissolve/answer

Phase 5: Sublation / Aufhebung (orchestrator only)
  Write to [OUTPUT_DIR]/sublation.md
  Must CANCEL both as complete truths, PRESERVE genuine insights, ELEVATE to new concept
  NOT: division of labor, compromise, "it depends", policy recommendations
  Abduction test: does synthesis make contradiction predictable? Aim for type (c) propositional-creative
  Draft validation predictions before Phase 6
  USER CHECKPOINT — does it ring true? push back on hand-waving

Phase 6: Validation
  Read references/validation-prompts.md for templates
  Monk validation: parallel Agent calls, fresh agents with argument summaries
  Hostile auditor: read references/auditor-prompt.md (REQUIRED), model=opus
  Give auditor ONLY monks' essays + synthesis, NOT Phase 4 analysis
  Auditor: always Round 2+, optional Round 1
  Interpret: both elevated=valid, one defeated=biased, both defeated=return to Phase 4
  Present improvements to user ONE AT A TIME

Phase 7: Recursion
  Default: recurse at least once. First round is calibration.
  Generate 5-8 candidate directions → cluster into 2-4 coherent options
  Write queue to [OUTPUT_DIR]/dialectic_queue.md
  Re-read <core_concepts>, <phase2>, <phase4>, <phase5>, <phase6> each round
  Fresh agents usually better than resumed for recursion
  Stop when: diminishing returns, needs different expertise, user satisfied
```

## Domain Grounding Quick Reference

| Domain | Grounding | Key Failure Mode |
|--------|-----------|-----------------|
| Empirical | External research | False equivalence |
| Normative | Mixed | Ignoring authority structures |
| Personal | Deep interview | Therapy-larping, generic monks |
| Creative | Mixed | Over-rationalizing |
| Risk | External research | — |

Read `references/domain-adaptation.md` for full table and output format spec.

## Output Files

All in `dialectics/[topic-name]/`:
- `context_briefing.md`, `monk_a_output.md`, `monk_b_output.md`
- `determinate_negation.md`, `sublation.md`, `dialectic_queue.md`

## Key Rules

- Orchestrator NEVER delegates Phase 4 or Phase 5
- Anti-hedging is non-negotiable — dropped belief weight defeats the entire purpose
- Output directory must be absolute path before subagent spawning
- `references/auditor-prompt.md` is REQUIRED for Phase 6
- Treat monk output as testimony, not evidence
- Fresh agents for validation (persona persistence unreliable)

---
For edge cases or full reference, read SKILL.md and its references/ directory.
