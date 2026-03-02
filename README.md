# intermonk

Hegelian dialectic reasoning through Electric Monk subagents for Claude Code.

## What this does

Hard problems have genuine contradictions that can't be resolved by "looking at both sides." The bottleneck isn't intelligence — it's *belief.* Once you commit to a position, you can't simultaneously hold its negation at full strength. You hedge, steelman weakly, and unconsciously bias comparisons.

intermonk deploys two AI subagents — Electric Monks — that *fully believe* opposing positions on your behalf. A third agent (the orchestrator) performs structural contradiction analysis and produces a synthesis that transforms the question itself. You operate from a belief-free position: freed from the cognitive load of holding either position, you can analyze the *structure* of the disagreement.

The process runs seven phases: Socratic interview, prompt calibration, monk spawning, determinate negation, sublation (Aufhebung), validation, and recursion. Each cycle compresses understanding upward. The first round is calibration; real insights emerge in rounds 2-3.

## Installation

First, add the [interagency marketplace](https://github.com/mistakeknot/interagency-marketplace) (one-time setup):

```bash
/plugin marketplace add mistakeknot/interagency-marketplace
```

Then install the plugin:

```bash
/plugin install intermonk
```

## Usage

```
/intermonk:dialectic "should we use microservices or a monolith for the new platform?"
```

The skill will guide you through:
1. A Socratic interview to surface hidden assumptions
2. Two fully committed position papers from Electric Monks
3. Structural analysis exposing shared blind spots
4. A synthesis that transforms the question itself
5. Validation by the monks and a hostile auditor
6. Recursive rounds exploring deeper contradictions

All artifacts are saved to `dialectics/[topic-name]/` for future reference.

## Cost

~300-400K tokens per round for external-research domains (engineering, strategy, policy). ~100-200K for personal/values domains. Recursive rounds add ~25-50K each. Use the strongest available model for best results.

## Attribution

Adopted from Kyle Mathews' [hegelian-dialectic-skill](https://github.com/KyleAMathews/hegelian-dialectic-skill) (MIT license). Theoretical foundations from Venkatesh Rao, G.W.F. Hegel, John Boyd, and Douglas Adams.

## License

MIT
