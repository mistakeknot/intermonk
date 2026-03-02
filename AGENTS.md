# intermonk — Agent Guide

Hegelian dialectic reasoning — Electric Monk subagents for structured contradiction analysis and synthesis.

## Canonical References
1. [`PHILOSOPHY.md`](./PHILOSOPHY.md) — direction for ideation and planning decisions.
2. `CLAUDE.md` — implementation details, architecture, testing, and release workflow.

## Philosophy Alignment Protocol
Review `PHILOSOPHY.md` during:
- Intake/scoping
- Brainstorming
- Planning
- Execution kickoff
- Review/gates
- Handoff/retrospective

For brainstorming/planning outputs, add two short lines:
- **Alignment:** one sentence on how the proposal supports the module north star.
- **Conflict/Risk:** one sentence on any tension with philosophy (or 'none').

If a high-value change conflicts with philosophy, either:
- adjust the plan to align, or
- create follow-up work to update `PHILOSOPHY.md` explicitly.

## Execution Rules
- Keep changes small, testable, and reversible.
- Run validation commands from `CLAUDE.md` before completion.
- Commit only intended files and push before handoff.

## Quick Reference

| Field | Value |
|-------|-------|
| Repo | `interverse/intermonk` |
| Namespace | `intermonk` |
| Manifest | `.claude-plugin/plugin.json` |
| Skills | 1 (`dialectic`) |
| Commands | 0 |
| Agents | 0 (monks spawned dynamically) |
| MCP servers | 0 |
| License | MIT |

## Release Workflow

```bash
scripts/bump-version.sh <version>
```

## Overview

**Problem:** Hard problems have genuine contradictions that can't be resolved by "looking at both sides." The bottleneck is belief — once you commit, you can't hold the negation at full strength.

**Solution:** Two Electric Monk subagents believe opposing positions at full conviction. The orchestrator performs structural contradiction analysis and synthesis (Aufhebung).

**Plugin type:** Single skill, no MCP server, no hooks.

**Current version:** 0.1.0

## Architecture

```
intermonk/
├── .claude-plugin/plugin.json
├── skills/
│   └── dialectic/
│       ├── SKILL.md                  # 7-phase orchestrator (~475 lines)
│       └── references/
│           ├── auditor-prompt.md     # REQUIRED — Phase 6 hostile auditor
│           ├── belief-burdens.md     # Phase 1c' — belief-burden typology
│           ├── domain-adaptation.md  # Domain types, failure modes, output format
│           ├── monk-prompt-template.md # Phase 2 — 7-section prompt template
│           ├── theory.md             # Optional — theoretical foundations
│           ├── validation-prompts.md # Phase 6 — monk validation + auditor orchestration
│           └── worked-examples.md    # Optional — prompt craft examples
├── README.md, CLAUDE.md, AGENTS.md, PHILOSOPHY.md, LICENSE
├── scripts/bump-version.sh
└── tests/structural/
```

Orchestrator flow:
```
Orchestrator (SKILL.md)
├── Phase 1: Elenctic Interview (with user)
├── Phase 2: Generate monk prompts
├── Phase 3: Spawn Electric Monks (2x Agent tool, parallel, run_in_background)
│   └── Decorrelation check after both complete
├── Phase 4: Determinate Negation (orchestrator only, reads monk files from disk)
├── Phase 5: Sublation / Aufhebung (orchestrator only)
├── Phase 6: Validation
│   ├── Monk A + Monk B evaluate (parallel Agent calls, fresh agents)
│   └── Hostile Auditor (Agent tool, fresh, uses auditor-prompt.md)
└── Phase 7: Recursion (user chooses direction)
```

SKILL.md uses XML-tagged sections (`<phase1>` through `<phase7>`) for selective re-reading during recursive rounds.

## File Output Structure

All paths resolved to **absolute** before subagent spawning.

```
dialectics/[topic-name]/
├── context_briefing.md
├── monk_a_output.md
├── monk_b_output.md
├── determinate_negation.md
├── sublation.md
└── dialectic_queue.md
```

Topic slug convention: lowercase, spaces to hyphens, max 40 characters. Date-prefix (`YYYY-MM-DD-`) recommended for disambiguation.

## Model Recommendations

- Use strongest available model for all phases (synthesis quality scales with capability)
- Heterogeneous models for monks increase creativity (different training data = different blind spots)
- Set via `model` parameter on Agent tool calls

## Domain Adaptation

| Domain | Truth Means | Good Synthesis | Grounding |
|--------|-------------|----------------|-----------|
| Empirical | What works | Testable criteria | External research |
| Normative | What's defensible | Tension map | Mixed |
| Personal | What aligns with priorities | Values clarification | Deep interview |
| Creative | What's interesting | Unexpected recombinations | Mixed |
| Risk | Actual risk structure | Decision framework | External research |

## Token Budget Reference

| Phase | External Domain | Personal Domain |
|-------|----------------|-----------------|
| Research (Phase 1) | 150-250K | 0-50K |
| Monk essays (Phase 3) | 25-45K | 15-30K |
| Analysis + synthesis (4-5) | 15-30K | 15-30K |
| Validation + auditor (6) | 17-40K | 17-40K |
| Recursive round (7) | 25-50K | 25-50K |
| **Total (1 round + recursion)** | **~300-400K** | **~100-200K** |

## Known Constraints

- Monks return text to orchestrator, which writes to disk. For long recursive sessions, selective reads prevent context flooding.
- `references/auditor-prompt.md` is a **required** operational artifact — Phase 6 cannot complete without it.
- First round is calibration; real insights emerge in rounds 2-3.
- Topic slug should be unique per session — use date prefix to prevent overwrite.
