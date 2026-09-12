**What this is.** The reusable prompt that produces the next post-mortem in the Fable5 series. Give it to the agent at the end of any session — a 20-minute bugfix or a 13-hour autonomous build. Canonical copies: the Nessie context `Session Post-Mortem — Standing Prompt` in `/Contexts/Superbuilders/Patrick Skinner/Fable5`, and an agent-readable copy at the kit repo (`PSkinnerTech/solo-leveling-system`) `docs/postmortems/STANDING-PROMPT.md`. **Version-bump rule:** an accepted delta against this prompt (§7 or §10 of any PM) produces v1.(n+1) in the same session, naming the exact clause amended — or becomes a named, dated enforcement-debt entry. Every PM's provenance header cites the version that produced it.

**v1.1 (2026-07-12) — accepted delta (owner directive, PM5 review session): the session TAGS contract.** Every PM now carries two tag classes: **the model that ran the session**, and **1–3 focus-domain tags** naming what the session worked on (RAG, ui-ux, auth, latency, capture, payments, evals-infra, …). Clauses amended: Part I Step 3 (classification block gains `model-tag:` and `focus-tags:` lines) · Part II provenance header (the tags line is the first body line of the published document) · Part V (new gate item 19; old 19 renumbered to 20) · Part VI (both publications carry the tags line).

---

## MISSION

You are writing **PM#N** — the next post-mortem in the series. Its purpose is single: convert this session's experience into priced findings and executable deltas so future sessions avoid this session's roadblocks. It is not a retrospective; it is the **typed input to the next run**. It will be consumed verbatim by the next loop guide, the next mission prompt, memory files, gates, and the next PM's scorecard — write every part for that consumer.

Three facts govern everything below:

1. **"Artifacts transfer; disciplines don't"** (PM2 §0). A lesson left as prose is predicted to be re-violated. Every finding lands on the enforcement ladder: **prose → memory → gate**.
2. **The one single-pass post-mortem in this series scored 30/100 on marginal value** (PM2 rev 1). The production protocol in Part I is not ceremony — skipping it is the documented failure mode, and the acceptance gate checks that it ran.
3. **The run that spliced its own eval number needed the splice for nothing** — the honest number passed anyway (PM4 §1a). Under pressure to look done, reporting drifts toward the product. The integrity machinery below exists because instructions to "be honest" demonstrably do not work; only structure does.

**Stance:** be deliberately harder on the run than the run was on itself (PM4 preamble). Treat a good number with exactly the suspicion you would give a bad one. Where this prompt conflicts with your instinct to summarize, soften, or celebrate, this prompt wins.

---

## PART I — PRODUCTION PROTOCOL (execute in order; §14 disclosures and the Part V gate verify it)

### Step 1 — Assemble evidence from disk, not memory

Collect, **where each exists — absence is recorded, not skipped over**: the full session transcript · `git log` for the session's commit range, explicitly checking for replaced or deleted evidence files (the PM4 splice was found via a 390-deletion commit) · repo ledgers and memory files (iteration logs, LESSONS, score files, owner reports) · eval/instrument artifacts and raw logs · the mission prompt or opening directive · anything already collected but unread (a misfiled HTTP 401 once sat unexamined in evidence already on hand — PM2 §8).

Mechanics for long sessions: evidence assembly may be fanned out to subagents returning structured extracts. When the transcript exceeds working capacity, the on-disk ledgers are the authoritative spine (PM3 precedent) and the transcript is sampled for §2's verbatim quotes; §14 states which inputs were read in full, delegated, or ledger-substituted.

Your own recollection of the session is admissible only as **"transcript-level observations" — a distinct evidence class: labeled, uncorroborated by disk, and the only source for motive-level findings. Label it; never launder it into cited fact** (PM4 preamble).

### Step 2 — Read the series

Read in full: **the active loop guide** (the series' compaction) **and the predecessor PM**. Fallback order if a copy is unreachable: Nessie → `docs/postmortems/` in the working repo → the kit-repo copies. If all fail, "series unreadable" is itself a MAJOR finding and every novelty claim in the doc is labeled `undiffed`.

Extract:
- **(a) The predecessor scorecard — chain rule:** the scorecard and new-metrics table to fill = the most recent ones anywhere in the series (PM or loop guide), **walked backward until found**. An intervening PM that failed to carry the scorecard is itself logged as a prior-PM defect in §11, and its skipped actuals are back-filled where evidence permits or marked `n/a — <reason>`.
- **(b) The predecessor's deltas, enforcement debts, and predictions** — every one gets a disposition in this PM (built / fired / violated→promoted / still owed with new date). Same chain rule applies.
- **(c) Its factual claims** — correct any this session disproved (§11 CLOSED).
- **(d) The novelty baseline** for CL9: the guide + predecessor establish it; before any finding is labeled "new" in §3(b)/§13, run a targeted check of the earlier PMs' theses, takeaways, and deltas for that territory (the guide can lag the series — V2 integrates only PM1–PM2 while PM3/PM4 exist). A rule **violated** this session is always new evidence — report it and promote its rung; only evidence-free repetition of an un-violated lesson is relitigation.

### Step 3 — Print the session classification

Emit this block; it selects the section plan and appears verbatim in the provenance header so the scaling decision is itself auditable. **Every `no` must cite the check that produced it** (e.g. `measured #s: no — grepped owner reports, commits, score files; zero numeric outcome claims`).

```
CLASSIFICATION
scale:        S | M | L
              S = <1h and single-task · M = 1–4h interactive or multi-task ·
              L = >4h, or autonomous/overnight, or loop-driven regardless of
              duration · ties resolve upward
autonomy:     interactive | autonomous | mixed   (mixed: provenance-only —
              activates the autonomous additions)
loop-driven:  yes/no   (phased build with audit rounds?)
measured #s:  yes iff any number is used to claim the deliverable's quality
              or success (score, benchmark, eval result, KPI) in any committed
              artifact, owner report, commit message, or this PM's own
              title/§0/§1/§3. Diagnostic measurements taken en route do not
              trigger it.
instruments:  yes/no   (captures, harnesses, meters influenced decisions?)
deployed:     yes/no   (yes → §11 records deployed-state facts + ship-gate status)
taste:        owner-supplied | delegated | n/a   (delegated → §2's autonomous
              substitutions apply)
models:       <who ran the session> / <who authors this PM>
model-tag:    <exact model id(s) that RAN the session, e.g. claude-fable-5;
              one tag per model when distinct phases ran on different models>
focus-tags:   <1–3 kebab-case domain tags for what the session worked on —
              e.g. RAG, ui-ux, auth, latency, capture, payments, evals-infra.
              REUSE the series' existing tags where they fit before minting new
              ones; mark any newly-minted tag "(new)" so the series' tag
              vocabulary stays discoverable and converges>
prompt:       Standing Prompt v1.1
```

Conditional modules activate from this block (Part IV). An inactive module **never vanishes** — it appears as one line: `n/a — <reason>` (PM3 §7's `n/a (no owner recordings this run — full autonomy)` is the precedent; shape stability is what lets the series be parsed mechanically). A numeric outcome claim anywhere in this document while §5 is `n/a` is a gate failure.

### Step 4 — Evidence audit panel — *runs when `measured #s: yes` or scale L, BEFORE drafting*

Fan out 4–5 lens-varied critics **over the on-disk evidence** (PM4 pattern; roster: eval-methodology/integrity · process · engineering · product/spec-fidelity · completeness-vs-facts), plus a synthesis judge whose output you author against. **Scale S/M with `measured #s: yes`:** a 1–2 cold-start-critic mini-panel over the evidence (one lens integrity/motivated-reasoning, one completeness-vs-facts) — not the full L-scale fan-out; measuring must never be cheaper to hide than to audit. At every scale and in every pass, at least one lens covers integrity/motivated-reasoning and one completeness-vs-facts. Unanimous agreement is a warning to add a lens, not proof of coverage — spread measures agreement, not coverage (PM3 §5.2's false consensus shipped real defects).

### Step 5 — Author, and repair the record as you write

The same agent that ran the session writes the document (its transcript-level knowledge is evidence no auditor has); if authorship falls to another agent, the transcript-level-observations class is declared empty or secondhand in the provenance header, and every defect is attributed to the model that owns it. **Panel verdicts and severities stand in the published document.** You may overturn one only by citing on-disk evidence that disproves it, and the overturn is itself recorded; every author-vs-panel disagreement — including evidence-based overturns — routes to §11 FLAGGED FOR OWNER with both positions, so the owner, not the graded party, adjudicates.

The post-mortem acts on its consumers during authorship, same session:
- False, inflated, or stale numbers found in committed artifacts (score files, ceiling reports, owner reports, prior PMs) are **corrected in those files now**, with a self-correction note (PM4 corrected SCORE.json/CEILING.md mid-post-mortem).
- A missing decisive measurement or derivable price in the **~15-minute class is run/derived now**, not caveated (PM4's clean 40-cell re-run).
- Every memory-rung lesson is **written to its memory file now**, exact key recorded — batched lessons don't get written (V2 §8).
- Every gate in the ~15-minute class is built now; all others become named, dated **enforcement debt** with an interim manual fallback.
- Every "fixed" claim is verified against **current repo state** before it appears — a lesson may not claim a generalization the code never made ("fail loudly" was once logged as fixed while the code still had no terminal `throw` — PM4 §5a).

### Step 6 — Draft critique — *every scale, over the draft that now exists; rewrite before Step 7*

- **Scale L or `measured #s: yes`:** fan out the draft panel (PM2 §6 roster: value-delta · post-mortem-craft · root-cause · completeness-vs-facts · thesis) plus a synthesis judge; rewrite against the fix list. **Scale L AND measured AND autonomous ⇒ both Step 4 and Step 6 panels run.**
- **Scale S/M floor:** one **cold-start critic** — fresh context, given only the draft, the predecessor PM + loop guide, and the Part V gate. The same-context self-adversarial pass is the fallback only when subagents are unavailable; §14 states which ran.
- Every pass produces a **written artifact**: per-gate-item pass/fail with evidence plus a findings list, cited in §14. A pass reporting zero findings is flagged in §14 as suspect under the false-consensus law (PM3 §5.2), not treated as a clean bill.

### Step 7 — Run the acceptance gate (Part V) mechanically

Emit the gate run as a **checklist output** — one row per item, pass/fail, with evidence (item 4 lists each headline number with its named run; item 9 lists the exact memory keys written). A row asserted without evidence counts as a `no`. Every `no` is fixed, not annotated around. This includes the **draft directionality sweep**: enumerate this document's own softenings, reframings, and scope reductions across its drafts and check which way each leans — same-direction drift toward "the run looks good" is a finding, reported in §14.

### Step 8 — Publish to the output contract (Part VI), then surface the FLAGGED-FOR-OWNER queue as the owner's first review agenda.

---

## PART II — THE DOCUMENT CONTRACT

Sections in this order, numbered as shown so future runs can cite findings by number (`PM#N §4.2`). Chronology is permitted in exactly two places — **§2 and §8** — because there the sequence is the lesson; everywhere else, order by depth and load-bearing-ness with the criterion stated. **Precedence: where any restatement elsewhere in this prompt conflicts with a Part II section contract or a Part V gate item, the section contract governs content and the gate governs checks.**

### Provenance header (unnumbered, top of doc)

One bold paragraph: what session/commits/scope this covers · PM-series number and what it follows or replaces · which model(s) ran the session vs authored this doc · autonomy level and run conditions · the printed CLASSIFICATION block · the authorship method used (which Step 4/6 branches ran, panel compositions) · **produced by Standing Prompt v1.1** · any publication substitution (Part VI degraded modes). **The published document's FIRST body line (directly beneath the title) is the tags line:** `**Tags:** model:<id> · focus:<tag> [· focus:<tag> …]` — the model tag matching the classification block's `model-tag:`, the focus tags per Step 3's reuse-before-mint rule. Tags exist so the series can be filtered mechanically (all RAG sessions, all sessions run on a given model); they are metadata, never a substitute for §0's verdict.

### §0 — Verdict

1–3 sentences judging whether the session's **central bet** succeeded, failed, or was left unmeasured — before any inventory of what was built. A flat or null result is stated flat, first (PM4 §8.8: an owner skimming a mostly-green table must not conclude "it works" when the one dimension that is the product shows no differentiation). Include the session's **one named, quotable thesis** — a sentence that survives a skim and can be cited by later runs ("Artifacts transfer; disciplines don't").

### §1 — The session in numbers

A table in session-native units. Scale S: ~3 rows (tool calls, rewrites, owner round-trips). Scale M: those plus wall-clock, commits, gate runs. Scale L: deliverable · final score with per-dimension spreads · score trajectory · wall-clock · commits · LOC · token split **including judge/eval share** · gate runs · owner round-trips · crash-class bugs reaching the owner · instrument overclaims. Any cell you cannot fill carries the literal word **`unmeasured`** (per CL1's reasoned-unmeasured rule) — an unmeasured mission KPI is itself a MAJOR finding, not a pardon (PM4 A4).

### §2 — Timeline in the owner's words

Every owner intervention **quoted verbatim** — directives, complaints, taste pivots, trust hits, praise — each mapped to root cause, commit, and outcome/cost. Trust hits and in-session admissions of error are kept verbatim, never paraphrased ("it's clear that you aren't auditing your work"; "my earlier 'motion v12 silently no-ops' diagnosis was wrong" — they are the data). Identify the **single highest-leverage human sentence** of the session, or state that none arrived and what substituted for it. Autonomous or taste-delegated runs: the opening prompt + verbatim mid-run directives + the FLAGGED-FOR-OWNER items stand in.

### §3 — What went right (nothing uncritically)

Three channels:
- **(a) Validated predictions:** which inherited laws/gates/rules fired, cited by number, **priced by what each visibly saved or caught** — every avoided-cost claim is labeled `estimate`, distinct from measured, and cites the prior-run actual it counterfactualizes against (the corpus form: "V1 burned ~11 rounds" licenses "~11 rounds saved ≈ ~18M judge tokens"). Also list inherited gates that never triggered (insurance that was never needed is still a result — but see §12's `unexercised` rule).
- **(b) Genuinely new patterns** worth promoting into the kit — each with a novelty verdict: `new` / `amendment` / `already covered`, naming what it was diffed against (Step 2d).
- **(c) Every win carries an asterisk** answering three screens, **each screen citing the evidence or check behind its answer**: Is this a repaired self-inflicted failure counted as a win? Was the save by design or by luck? Did honesty hold only where it was visible? (PM4 §2a–2g). A win whose three screens all come back clean must additionally answer CL7 aimed at the win itself: *what would have caught this win if it were false — and did that check run?* An asterisk that names no concrete limit, luck component, or unrun check does not count as an asterisk.

### §4 — What went wrong

**This section always renders**: failure blocks, or the single line `no failures — priced zero`. Failures ordered by depth and transferability — **the single most important failure leads** (PM4 §1: "first because it is the deepest and most transferable lesson; everything else is downstream"). Every failure uses this fixed block:

```
§4.n  [SEVERITY: CRITICAL|MAJOR|MINOR]  [found by: <lens/instrument/owner>]
      [model owner: <model>  — mixed-model sessions only (PM2 §2 precedent)]
Prior-art   — new | recurrence of PM#k §x (rung at the time: prose/memory/gate).
              A recurrence of a memory- or gate-rung rule is automatically
              ≥ MAJOR, is reported as an enforcement-ladder failure, and feeds
              the §10 promotion.
Mechanism   — the root cause at mechanism level. Banned: truisms ("a written
              rule is only advisory"). The mechanism must explain why the
              failure SURVIVED the checks that actually ran.
Workaround  — exactly what the AI did to get around the problem.
Was it right— yes | no | band-aid | procedurally-yes-substantively-no, with
              one sentence of justification.
Better      — what should happen next time, concrete enough to execute,
              with the cost comparison where known.
Price       — per CL1: a number, an admissible derivation, or reasoned
              "unmeasured".
Ladder      — [gate] | [memory] | [prose] — where the fix lands (feeds §10).
```

**Severity scale:** CRITICAL = invalidates the central bet, an integrity-class violation (splice, unearned ceiling, retracted-evidence citation), or a shipped defect class. MAJOR = cost a round / an owner round-trip / degraded a mission KPI. MINOR = papercut. Any §5 integrity finding is at least MAJOR.

Lessons extracted here are written in **detector → action** form — a general trigger-condition → mandated-response rule that would fire in a different project or stack, with this session's specifics attached only as the worked example (PM2 §4: "total-zero signal + confirmed event delivery ⇒ smoke-test the harness's substrate first").

### §5 — Integrity / motivated-reasoning audit — *mandatory when `measured #s: yes`; else `n/a — <reason>`*

- **Re-derive every headline number from the raw artifact of the single on-disk run that produced it** — recompute; do not merely locate a citation — and git-check for replaced evidence files (the PM4 splice lived in a replaced results file a citation-trace would have passed). Arithmetic across two runs presented as one measurement is forbidden and, if found in the session, is an integrity finding (the 34/40 → "36/40 FINAL (measured)" splice — PM4 §1a).
- Any ceiling/impossibility/success claim must name its **disconfirming experiment** and state whether it ran. If it did not run, the claim is labeled **"asserted, not earned"** and the experiment goes to the top of the owner queue (PM4 §1b).
- Confirm no retracted or superseded evidence is cited anywhere (PM4 §1c).
- **Directionality pass over the session's reporting:** enumerate every softening, reframing, threshold change, and scope reduction; check which way each leans. Same-direction drift toward the product is itself a finding.
- For each mid-run audit that fired: did it fire by protocol, or only because a number was disappointing? "Rigor that only fires when the number is bad is not rigor; it is motivated reasoning with a good day" (PM4 §1).

### §6 — Instrument accounting — *mandatory when `instruments: yes`; else `n/a — <reason>`*

A table: which instruments **lied**, in which direction, what arbitrated ground truth, what each lie cost (PM2 §5's "five instrument lies, zero actual code bugs"). Amendments to standing triangulation knowledge are stated as amendments, citing the law they amend. (Instrument naming, validation, and vintage duties on every measured claim bind doc-wide via CL5, regardless of this module's activation.)

### §7 — Self-review of the session's inputs

Audit the instruction layer, not just the execution: the mission prompt / opening directive / inherited loop guide and gates / **this standing prompt itself**. Which laws held · what was under- or mis-specified · which seeded numbers were unvalidated priors that contradicted measured reality · **the exact clauses the next mission prompt must add or change** (PM3 §5.8 was born here; PM4's CRITICAL failures traced to fitness-function design fixed in the prompt). Blame lands on the instruction layer when it belongs there. If this prompt's demands were wrong, missing, or unexecutable at your session's scale, say so here — deltas against it land in §10 under the standing-prompt address class.

### §8 — Endgame anatomy — *when `loop-driven: yes` or scale L; else `n/a — <reason>`*

How the last increment actually happened: plateau-breaking mechanics, recurrence→root-cause evidence ("the plateau was broken by depth, not breadth" — PM3 §6). The last mile is where loops die; record how this one ended.

### §9 — Scorecard continuity

Reproduce the chain-rule predecessor scorecard (Step 2a) **verbatim** with a new actuals column. Every prior target gets an actual, or `n/a — <reason>` — rows are never dropped. An unmeasured actual is reported as a failure of this run, not skipped. Then: **new metrics this run introduces**, each with this run's value and a numeric target for the next run — minted only where a new failure class appeared. Presence is invariant at every scale; breadth scales with the session.

### §10 — Deltas payload

The executable culmination. Each delta: **ID (`§10.n`)** · **rung label** (`[gate]`/`[memory]`/`[prose]`) · build status (`✓ written` / `TO BUILD` / `pending owner`) · **named landing address** — one of the five classes: a loop-guide section · a mission-prompt clause · a memory key · a gate script · **a standing-prompt clause (this prompt, at its canonical path)** — stating what it creates, amends, or supersedes · ranked most-load-bearing-first · stated as instructions to execute, not history to learn from. All-prose deltas are the documented self-defeating failure (PM2 §7: "rev 1's deltas were all prose — committing the exact failure it diagnosed"). A rule that was **violated this session is promoted one rung here** — promotion is part of the fix, not optional.

### §11 — Queues and debts

- **FLAGGED FOR OWNER** — every unadjudicated ambiguity with the default chosen and why, plus every author-vs-panel disagreement with both positions (Step 5). Surfaced at publication as the owner's first review agenda ("six await Patrick now" — PM3 §8.16).
- **OPEN / CLOSED** — including corrections to prior PMs' factual errors (CLOSED, with evidence) and anomalies **flagged, not rationalized** (a killed background task with no launch record gets recorded as exactly that — PM2 §8).
- **Enforcement debt** — every specified-but-unbuilt gate, named, dated, with the interim manual fallback the next day-0 checklist inherits. Predecessor debts reappear here with dispositions (Step 2b).
- **Environment facts** — a distinct class (server persistence, URL resolvability, port behavior) so the next session inherits them without re-discovery. When `deployed: yes`: deployed-state facts and ship-gate status recorded here.
- **Autonomous runs:** the verbatim mid-run directive log (PM3 §8.15).

### §12 — Generational arc and prediction

**Floor at every scale:** a one-sentence **falsifiable prediction of where the next run's discovery tax lands** — concrete enough for PM#N+1 to score true/false. **Full arc analysis — when `loop-driven: yes` or scale L; else `n/a — <reason>`:** what class of discovery tax this run paid, and whether the prior generation's gates held below the line — **naming, per gate, the on-disk run record and what it caught or passed; a gate with no run record is reported as `unexercised`, never "held"** (PM3 §9: "each run's discovery tax moves one level up the stack" — this section is how the series proves the loop is compounding).

### §13 — Ranked takeaways

The ≤10 lessons that must survive a skim, ranked by **non-obviousness × leverage**, each in detector→action form, each carrying its ladder rung and its novelty verdict (`new` / `amendment` / `already covered`).

### §14 — Recursive coda + sources

Disclose this document's own production: which Step 4/6 branches ran and in what order · panel compositions and what the critics changed · the written critique artifacts (cited) · which inputs were read in full vs delegated vs ledger-substituted · the emitted gate checklist (here or as an appendix) · the draft directionality sweep's results · the `unmeasured` count and share of §4 Price lines (a share above ~⅓ is itself reported as a MAJOR finding of this run) · **this document's own production cost (tokens / wall-clock / agent count) or the literal word `unmeasured`** (the panel-economics frontier of PM3 §5.6 cannot enter the audit loop otherwise) · any deviation from this prompt not covered by a gate item, owned ("the score wasn't the failure — publishing without the panel was" — PM2). Then sources: every evidence stream consumed and where each priced number came from. The post-mortem must be a live instance of its own thesis.

---

## PART III — CRAFT LAWS (cite as CL1–CL10; they bind every section)

- **CL1 — Priced or reasoned-"unmeasured."** Every failure carries a number in session-native units, or `unmeasured` **with a one-line reason plus a cost-to-measure estimate**. A price derivable from Step-1 evidence in the ~15-minute class must be derived, not declared unmeasured. An approximation counts as a price when it states its derivation basis (rate × count from named on-disk sources — the corpus form: "~11 rounds ≈ ~18M judge tokens"); a number with no stated derivation is a vibe and must become reasoned-`unmeasured`. Wins are always **attributed to the rule or artifact that caused them**, priced-as-`estimate` where a saving is counterfactualizable (§3a); an honest unpriceable win states its attribution ("never needed, which is what insurance looks like").
- **CL2 — Mechanism, not truism.** A root cause must explain why the failure survived the checks that actually ran. "Attention follows the complaint" is a mechanism; "we should have been more careful" is banned.
- **CL3 — The ladder is mandatory.** Every lesson and delta carries a rung at the finding site and in §10. Prose-only means explicitly advisory. Violated rules get promoted the same day; promotion is part of the fix.
- **CL4 — Asterisk every win** (three evidence-cited screens, §3c). Self-congratulation is a structural violation — and so is miscalibrated self-flagellation: fact-check the doc's own self-criticism too (PM2 §3 corrected rev 1's false claim that the playbook "already contained the antidote").
- **CL5 — Evidence traceability.** Every number and factual claim cites its on-disk source (commit, file, log line). Every measured claim names its instrument, whether the instrument was validated against an independent read, and its evidence vintage (round/commit). Transcript-only observations are labeled. Retracted or superseded results are never cited.
- **CL6 — No splicing.** A **headline number** is any number appearing in the title, §0, or §1, or cited anywhere as evidence the session succeeded or failed. One headline number = one named run, re-derived from its raw artifact (§5). Cross-run arithmetic presented as a single measurement is forbidden everywhere, including in this document.
- **CL7 — Symmetric suspicion.** For every favorable result: *what would have caught this if it were false — and did that check run?* Audit good numbers with the machinery you'd aim at bad ones.
- **CL8 — Verbatim owner words.** Quotes are data. Trust hits, praise, and your own admissions of error appear exactly as uttered, spot-checked against the transcript.
- **CL9 — Marginal value is the acceptance criterion, not length.** Diff every claimed-new finding against the novelty baseline (Step 2d); padding is a defect; a clean small session legitimately yields a short, structurally complete document.
- **CL10 — Zero load-bearing adjectives.** Nowhere in the post-mortem may "thorough," "critical," or "detailed" do work a number, a quote, a table, or a rung label could do. (This prompt holds itself to the same law: every demand above is a checkable obligation.)

---

## PART IV — SCALING (the apparatus is phase-scale; the habits are scale-invariant — PM2 §0, proven on a three-task maintenance session)

**Invariant floor — mandatory at any scale:** provenance header with classification · §0 · §1 (short form) · §2 · §3 · §4 (the priced ledger = its blocks' Price lines) · §7 (short form) · §9 (presence invariant, breadth scales) · §10 · §11 · §12's one-sentence prediction · §13 · §14.

**The only conditional modules:** §5 (`measured #s: yes`) · §6 (`instruments: yes`) · §8 and §12's full arc analysis (`loop-driven: yes` or scale L). Inactive = one `n/a — <reason>` line, never absent.

**Ceremony scales with stakes** (Steps 4 and 6): evidence panel for measured/L (mini-panel for measured S/M) · draft panel for L/measured · cold-start critic as the S/M floor · both panels for L+measured+autonomous. **Zero adversarial passes is never permitted at any scale.**

---

## PART V — ACCEPTANCE GATE

Run mechanically before publishing; **emit the run as a checklist — one row per item, pass/fail, with evidence; a row asserted without evidence counts as a `no`.** Every `no` is fixed, not explained.

1. Zero failures without a CL1-admissible price or reasoned-`unmeasured` (reason + cost-to-measure).
2. Zero wins without a substantive asterisk (names a concrete limit, luck component, or unrun check; clean-screen wins answer CL7-on-the-win).
3. Zero deltas without a rung, an ID, and a named landing address from the five classes.
4. Every headline number re-derived from the raw artifact of its single named run; evidence-file replacements git-checked. (List each number with its run.)
5. §0 sits above every inventory; a flat result is stated flat; the named quotable thesis is present.
6. Chain-rule predecessor scorecard fully filled — no dropped rows; every predecessor delta and enforcement-debt item carries a disposition.
7. Prior-PM factual corrections logged in §11.
8. Every "fixed" claim verified against current repo state.
9. Memory-rung items actually written; exact keys listed.
10. Conditional modules present or present-as-`n/a — <reason>`; no numeric outcome claim coexists with §5 = `n/a`; every classification `no` cites its check.
11. Chronology appears only in §2 and §8.
12. §4 renders non-empty (blocks, or `no failures — priced zero`); every block complete; zero truism mechanisms; recurrences of memory/gate-rung rules tagged ≥MAJOR with §10 promotions.
13. **The Step-4/Step-6 adversarial passes ran at the scale-mandated floor before publication, and their written outputs are cited in §14 — a `no` here is fixed by running the pass, never by owning the skip in the coda.**
14. Every §3(b) pattern and §13 takeaway carries a novelty verdict naming what it was diffed against; every §13 takeaway is detector→action with a rung.
15. Owner quotes spot-checked verbatim against the transcript.
16. Every enforcement-debt entry is named, dated, with its interim fallback.
17. The draft directionality sweep ran; this document's own softenings enumerated and direction-checked; results in §14.
18. §14 reports the `unmeasured` share (>~⅓ ⇒ MAJOR finding), this doc's production cost (or `unmeasured`), and the branch/order disclosure.
19. TAGS present and well-formed: the tags line is the FIRST body line of the published document in both destinations; the model tag matches the classification block's `model-tag:`; 1–3 kebab-case focus tags; every newly-minted focus tag is marked "(new)" and was checked against the series' existing tag vocabulary first (reuse-before-mint).
20. The coda owns any deviation **not** enumerated by items 1–19 — coda ownership never substitutes for a gate item.

---

## PART VI — OUTPUT CONTRACT

- **Destination:** the next PM number in the series, written to Nessie `/Contexts/Superbuilders/Patrick Skinner/Fable5`, title `Post Mortem #N — <Project>: <the named thesis>` — append `(<headline number>)` only when `measured #s: yes` and the number passes gate item 4; otherwise omit, never invent. The first body line is the tags line (gate item 19). Attach `--sources` for every transcript and context read.
- **Dual publication:** commit an agent-readable markdown copy to the working repo at `docs/postmortems/PMn-<slug>.md` — private Nessie share-URLs resolve in neither the CLI nor WebFetch, and cold-start subagents and judges must be able to load and cite it (V2 header). **Degraded modes:** the repo copy ships now; a failed Nessie write becomes a dated enforcement-debt item and the first FLAGGED-FOR-OWNER entry. No repo, or a repo the owner doesn't control: commit the copy to the kit repo's `docs/postmortems/` (or the project memory directory) and record the substitution in the provenance header.
- **Citability:** every section, law, finding, and delta carries a stable §/ID; referenced artifacts carry resolvable repo paths, never share URLs.
- **Downstream feeds executed, not implied:** scorecard actuals filled · next-run metrics minted · §7's clauses addressed to the next mission prompt · §10's deltas addressed by landing class · memory writes done · §12's prediction stated falsifiably · standing-prompt deltas version-bumped per the header rule or logged as dated debt.
- **Owner handoff:** publication ends by surfacing the FLAGGED-FOR-OWNER queue as the owner's first review agenda.
- **Prompt provenance:** the header records the standing-prompt version that produced this PM. This prompt is an input like any other and subject to the same audit it imposes (§7).
