# intermonk

Hegelian dialectic reasoning through Electric Monk subagents. Adopted from [hegelian-dialectic-skill](https://github.com/KyleAMathews/hegelian-dialectic-skill) (Kyle Mathews, MIT).

## Skill

- `/intermonk:dialectic "topic or tension"` — Run structured dialectical analysis

## How It Works

Two subagents (Electric Monks) fully commit to opposing positions. The orchestrator performs structural contradiction analysis (determinate negation, Boydian decomposition) and produces synthesis (Aufhebung) that transforms the question itself. User operates from a belief-free position.

## Output

All artifacts written to `dialectics/[topic-name]/` relative to working directory:
- `context_briefing.md` — research and user context
- `monk_a_output.md`, `monk_b_output.md` — fully committed position papers
- `determinate_negation.md` — structural analysis
- `sublation.md` — synthesis
- `dialectic_queue.md` — recursion queue for future rounds

## Cost Expectations

- External-research domains (engineering, strategy, policy): ~300-400K tokens per round
- Personal/values domains (life decisions, career): ~100-200K tokens per round
- Recursive rounds add ~25-50K tokens each

## Design Decisions (Do Not Re-Ask)

- Orchestrator never delegates Phase 4 (determinate negation) or Phase 5 (sublation) — requires continuity with the elenctic interview
- Fresh agents for validation, not resumed sessions — persona persistence is unreliable
- Monks return text to orchestrator, which writes to disk — prevents context flooding in recursive sessions
- `references/auditor-prompt.md` is a required operational artifact, not optional reference
- Anti-hedging language is functional, not stylistic — preserved verbatim from source
- Output directory resolved to absolute path before subagent spawning

## Validation

```bash
cd tests && uv run pytest -q
```
