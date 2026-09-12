---
name: postmortem
description: Use when a software or agent session, incident, deployment, evaluation, autonomous run, bugfix, or project phase has ended and needs an evidence-grounded post-mortem, root-cause analysis, scorecard continuity, executable deltas, or a publication-ready Fable5 PM-series artifact.
---

# /postmortem

## Core rule

Convert session evidence into priced findings and executable deltas that change the next run. Apply the governing principle: **artifacts transfer; disciplines do not**. A lesson left only as prose is predicted to recur.

## Load the complete contract

Read [references/standing-prompt-v1.1.md](references/standing-prompt-v1.1.md) completely before gathering evidence, drafting, or publishing. It is the normative contract; do not substitute a generic retrospective.

**REQUIRED SUB-SKILL:** Use `nessie` to read or publish Nessie material.

When reachable, compare the bundled snapshot with the canonical Nessie context named `Session Post-Mortem — Standing Prompt`. Use the newer complete version, never mix versions, and record the producing version in the provenance header. Fall back to the bundled v1.1 snapshot when Nessie is unavailable.

Explicit user constraints such as `read-only` or `draft-only` override publication side effects, but never evidence integrity. Record the resulting contract deviation exactly as the standing prompt requires.

## Execute

1. Establish the repo, session boundary, commit range, transcript or ledger, next PM number, predecessor PM, loop guide, deployment state, and models that ran versus authored the session. Resolve discoverable facts instead of asking the user to repeat them.
2. Execute Part I in order. Read on-disk evidence, prior-series material, raw measurements, owner words, and current repo state. Record missing evidence; label recollection as transcript-level observation.
3. Print the exact classification block. Let it activate the required panels and conditional modules. Scale ceremony and breadth, never the invariant section floor.
4. Author in Part II order under the craft laws. Correct false committed claims, write memory-rung lessons, build short-class gates, and record longer work as named, dated enforcement debt with a fallback.
5. Emit all 20 Part V gate rows with evidence. A failed or unsupported row blocks publication; fix it rather than explaining around it.
6. Unless the user requested a non-publishing mode, write the next PM to Nessie and commit the repo copy to the required destination. Surface `FLAGGED FOR OWNER` first.
7. Hand off with destinations, prompt version, gate result, unresolved owner items, and fresh verification evidence. Do not stop at a plan.

## Pressure checks

| Temptation | Required response |
| --- | --- |
| Owner says “fixed” | Preserve the quote, then verify current repo and deployed state. |
| Two runs average to a better headline | Keep them separate; one headline number comes from one named raw run. |
| A good score makes evidence loss secondary | Treat replaced, stale, or unvalidated evidence as an integrity finding. |
| The session was small and clean | Keep every invariant section; render `no failures — priced zero` only after audit. |
| A prior PM already documented the rule | Dispose the delta; a recurrence promotes the rule one rung and is at least MAJOR when it recurs from memory/gate. |
| Deadline or agent capacity blocks the adversarial floor | Return a non-publishable draft with the failing gate; never manufacture a pass. |

## Example

For `/postmortem the 45-minute OAuth callback fix; the targeted test passed, but it was not deployed`, classify the run, distinguish a diagnostic test from a success metric, quote owner words, verify current state, render inactive modules as `n/a — <reason>`, run the cold-start critic and 20-row gate, then publish both artifacts or record the requested degraded mode.
