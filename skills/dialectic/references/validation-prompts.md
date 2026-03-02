# Validation Prompt Templates

**When to read:** Phase 6 (Validation by the Electric Monks). Use these templates to construct monk validation and auditor orchestration prompts.

---

## Monk Validation Prompt

Send a condensed summary of the synthesis to each monk. Spawn **both validation agents in parallel** (persona persistence is unreliable; include a summary of each monk's original argument):

```
Agent tool call 1 (parallel):
  description: "Monk A validates synthesis"
  subagent_type: "general-purpose"
  prompt: [VALIDATION PROMPT below, with Monk A's argument summary]
  run_in_background: true

Agent tool call 2 (parallel):
  description: "Monk B validates synthesis"
  subagent_type: "general-purpose"
  prompt: [VALIDATION PROMPT below, with Monk B's argument summary]
  run_in_background: true
```

**Validation Prompt:**

```
You argued passionately for [POSITION]. Here is a summary of your argument:
[CONDENSED SUMMARY OF THIS AGENT'S ESSAY]

A dialectician has proposed a synthesis. Here is the structural analysis:
[CONDENSED SUMMARY OF PHASE 4 — key moves only]

Here is the proposed synthesis:
[CONDENSED SUMMARY OF PHASE 5]

Evaluate honestly from your committed position:

1. Does this synthesis PRESERVE your core insight?
2. Does it reveal a genuine limitation you can now see?
3. Do you feel ELEVATED or DEFEATED? Be honest.
4. What's wrong with this synthesis?
5. DEFEASIBILITY: What single piece of evidence would force you to abandon
   even your ELEVATED position?

Do NOT be agreeable. If the synthesis is just compromise dressed up, call it out.
```

## Hostile Auditor Orchestration

After monk validation, spawn a hostile auditor — a separate agent whose sole mandate is to find what's wrong. **Use the prompt template from `auditor-prompt.md`** (that file is required — do not skip it).

```
Agent tool call:
  description: "Hostile auditor attacks synthesis"
  subagent_type: "general-purpose"
  model: "opus"  # Use strongest available
  prompt: [Auditor prompt from auditor-prompt.md, with monks' essays + synthesis inserted]
```

**Critical:** Give the auditor ONLY the monks' essays and the synthesis. Do NOT give it the Phase 4 analysis — it should attack from fresh eyes. DO include 2-3 sentences of domain context.

**When to use the auditor:**
- **Always in Round 2+.**
- **Optional in Round 1** — first-round synthesis is calibration and will be superseded.
- **Always when the synthesis feels too easy** or like it's splitting the difference.

## Critical ABS Insight

The monks don't *stop believing* after the synthesis. A defeated monk has dropped its belief load. A properly elevated monk *believes more* — it sees its original position as a partial truth within a larger truth.
