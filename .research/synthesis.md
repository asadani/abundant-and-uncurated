# Synthesis: data use in the AI age

44 claims, 42 passing, 2 failed. 27 snapshots, 23 distinct works, 12 T2 and 15 T3,
no T1 and no T4. Every claim and every conclusion is bound by exact quote to a
snapshot; 56 bindings, zero quote misses.

The seven conclusions are `c-100` through `c-106`.

---

## sq1 — Recursion: what happens when models train on model output

**Conclusion (`c-100`, stance mixed, confidence moderate).** Recursive training
degrades models under the regime where synthetic data *replaces* real data, and
not under the regime where it *accumulates* alongside it. The widely repeated
claim that training on model output causes collapse is true of a setup that does
not describe how models are actually trained.

**Converged.** That degradation is real in the replace regime is not in dispute.
`c-001` and `c-002` (Nature, T2) establish that models forget the true
distribution and that distributional tails disappear. `c-003` establishes that
test error rises with each iteration when data is replaced.

**Contested, and the disagreement is the finding.** `c-004` establishes that
accumulation avoids collapse; `c-005` establishes that the literature carries
eight different definitions of the degradation it is arguing about. The sources do
not contradict each other on fact — they study different regimes. Nature studies
replacement; Gerstgrasser et al. add the accumulation arm; the position paper
observes that the replace paradigm zeroes out real data after one iteration
(`c-006`) and so describes no real training pipeline.

**A tier inversion worth stating in the paper.** The peer-reviewed T2 source
carries the *less* qualified claim, and the T3 preprints carry the more careful
one. Recency, not review status, is doing the work. A reader who weights by venue
alone gets this backwards.

**Correction check.** The Nature paper has a 2025 Author Correction (`c-007`). It
amends a symbol in the Theoretical intuition section. It is not a retraction and
does not affect the findings. Recording this because the lens flags uncorrected
citation of corrected papers as a trap, and because a paper this heavily cited
attracts the assumption that the correction must have been substantive.

---

## sq1 (mechanism) — What the exogenous signal has to be

**Conclusion (`c-101`, stance supported, confidence moderate).** What prevents
degradation is signal *exogenous to the system that produced the data*. A stronger
model can supply it — but only up to that model's own knowledge, which makes human
signal the only source not bounded by an existing model.

This is the load-bearing wall of the whole argument, and it was nearly missed.

`c-009` gives the mechanism: data must be "curated in some way to inject signal
that is exogenous to the system that produced the original data." Note what that
does *not* say — it says exogenous, not human.

`c-010` then appears to close the door on the human: a verifier "whether a human or
a better model" prevents collapse. Read at abstract level, that makes humans
replaceable by a stronger model.

Reading two sentences further inverts it. `c-036`: gains "plateau and may even
reverse" unless the verifier is perfectly reliable. `c-037`: verifier-guided
retraining "ultimately drives the parameter estimate to the verifier's knowledge
centre." A model verifier does not add information to the system — it transfers
information the verifier already has, and then the process stops. The human is not
in the loop as a quality control step; the human is in the loop as the only
unbounded source of new information.

**Single-source risk, stated plainly.** The knowledge-centre result rests entirely
on `s-018`, a T3 preprint whose long-run analysis is theoretical (linear
regression, a VAE on MNIST, a 135M-parameter LM). If that source is withdrawn or
fails to replicate at scale, this conclusion degrades from a formal result to a
plausibility argument. It is the most important and least corroborated claim in
the corpus.

---

## sq2 — Where synthetic data genuinely works

**Conclusion (`c-102`, stance supported, confidence low).** Synthetic data improves
models conditionally, not generally, and the binding condition is the *strength of
verification* applied to it, not the volume generated.

**Converged.** `c-011`: filtering helps "only when the underlying verification is
strong enough to provide a high-resolution correctness signal." `c-013`: measured
diversity correlates with downstream performance. `c-014`: seed data quality
matters more than novelty.

**A correction to the common practitioner claim.** The received wisdom — including
in the material this project inherited — is that a judge filter is *the* critical
step and that an unfiltered synthetic dataset is worse than a smaller filtered one.
`c-012` complicates this: naive or rigid verification filtering produced *no
improvement at all*. Filtering is not automatically virtuous. Weak filtering is
theatre, and over-strict filtering removes the diversity that `c-013` says you need.

**Confidence is low by the weakest-link rule**, not by an averaging of the
evidence. `c-014` comes from a vendor with a direct commercial interest in the
finding that curation beats scale. And `s-011` is code-only — a domain where a
compiler supplies free ground truth, which makes it the most favourable possible
setting for automated verification and the least representative of tone, safety or
domain nuance. This conclusion should not be carried into non-verifiable domains
without that caveat attached.

**The disconfirming case, presented rather than managed.** `c-015`: a self-play
system trained with no human-curated data beat models trained on expert-curated
human data in coding. That is real and it is the strongest evidence against the
paper's thesis. Three things bound it. The margin is **0.3 percentage points**
(`c-035`) — a near-tie, not a rout, and the abstract-level framing obscures this.
It works because a code executor supplies verifiable feedback (`c-016`), which
exists for code and mathematics and does not exist for tone. And the paper itself
concedes that "zero-data" methods still depend on expertly curated question
distributions.

---

## sq3 — Why curation stays expensive

**Conclusion (`c-103`, stance supported, confidence moderate).** Human curation is
costly for structural reasons, not temporary ones: the volume required is
continuous rather than one-off, the failures it prevents are delayed and hard to
detect, and the process encodes contested judgement rather than recording facts.

This is the sub-question the user's prior was about, and the evidence supports it
while sharpening it in a way the prior did not anticipate.

The prior said curation is expensive because it takes effort, time, process and
quality-control standards. True, and `c-020` gives the magnitude: a frontier
alignment pipeline collecting preference data *weekly*, over a million binary
comparisons. That is not a dataset built once; it is a standing operation.

But volume is the least interesting half. Two findings explain why the cost does
not fall with better tooling:

- **Failure is invisible until late.** `c-019`: data cascades are "opaque and
  delayed, with poor indicators and metrics." `c-017`: 92% of practitioners
  surveyed (n=53) hit at least one. You cannot cheaply quality-control a process
  whose defects only surface downstream, because the feedback signal you would
  automate against does not exist at the time of the work.
- **Curation is normative, not clerical.** `c-022`: annotation instructions
  "reproduce and normalize the worldviews of requesters." Curation is not
  transcription of a fact that a cheaper worker could transcribe equally well. It
  encodes a position. That is why quality standards are expensive to write and
  contested to apply — and why `c-021` (workers paid cents per task, without
  employment protection) describes a cost that has been *displaced* rather than
  eliminated.

**Checked and absent.** No peer-reviewed cost-per-label figure for *expert*
curation was found. `c-028` gives a real comparison — under $0.003 per annotation,
about thirty times cheaper than MTurk — but the human baseline there is crowd
workers on classification, which is not the expert judgement this conclusion is
about. This is the thinnest arm of the corpus and the report must say so.

---

## sq4 — Whether automated judgement can replace human judgement

**Conclusion (`c-104`, stance mixed, confidence moderate).** Automated judgement
can substitute for the *graded labour of applying* criteria, but not for the
*formation* of criteria, because criteria cannot be fully specified before humans
have looked at outputs.

**The disconfirming evidence is strong and goes first.** `c-023`: strong LLM judges
agree with human preferences at over 80%, matching human-human agreement. `c-027`
(PNAS, T2): ChatGPT beat crowd workers by about 25 percentage points. `c-028`: at
roughly one-thirtieth the cost. Anyone arguing that humans are irreplaceable has to
get past these, and averaging them away would be exactly the well-cited misleading
move this pipeline exists to prevent.

**The reconciliation is a distinction of kind, not degree.** Every one of those
results measures performance *against a fixed rubric*. `c-025` shows the rubric is
the part that cannot be fixed in advance: it is "impossible to completely determine
evaluation criteria prior to human judging of LLM outputs." `c-026` names the
circularity — you need criteria to grade outputs, and grading outputs is how you
discover the criteria. The UIST study observed participants revising criteria even
after grading first, and going back to change earlier grades.

This matters because it is a *structural* argument, not a capability argument. It
does not say models are not yet good enough at judging. It says the specification
of what counts as good cannot be completed before the looking happens. A better
model does not dissolve that; it only makes the applying cheaper once the looking
is done.

`c-024` adds the practical caveat that the same paper reporting >80% agreement also
documents position bias, verbosity bias, self-enhancement bias and limited
reasoning. The headline figure and the bias taxonomy come from one source and
should always be cited together.

---

## sq5 — Whether high-quality human data is actually running out

**Conclusion (`c-105`, stance supported, confidence moderate).** The shortage is
partly a *forecast* about absolute supply and partly an *observed withdrawal of
access* — and only the second is currently measurable.

`c-031`: models will be trained on datasets roughly equal to the stock of public
human text between 2026 and 2032. That is a projection, from Epoch AI, an
organisation whose visibility depends on scaling forecasts being newsworthy. It has
not been observed.

`c-032`: more than 28% of the most actively maintained, critical sources in C4 are
now fully restricted via robots.txt. That is a measurement, from an independent
group, of something that already happened.

These are two different phenomena and the paper should not blend them. Exhaustion
is a supply problem that better curation could in principle address. Consent
withdrawal is a governance problem that no amount of curation effort can fix,
because the data still exists and is simply no longer available. The scarcity in
"abundant but not curated" is, at least in part, not scarcity of *text* — it is
scarcity of *permission*.

---

## Overall answer

**`c-106` (stance mixed, confidence moderate).** Machines scale the application of
judgement; humans remain the source of the judgement being applied. Two independent
mechanisms converge on this:

1. A synthetic loop converges on what its verifier already knows (`c-037`), so a
   closed loop of models cannot generate genuinely new information about the world.
2. Evaluation criteria cannot be fully specified before outputs are seen (`c-025`),
   so the definition of quality cannot be handed over in advance.

The user's opening framing — "synthetic data is scaling HITL, not sunsetting it" —
survives verification, but the reason it survives is not the one the inherited
material gave. The inherited argument was that humans are better at certain
judgement tasks. The evidence does not support that as stated; `c-027` shows a
model beating crowd workers decisively. The argument that does survive is
informational and structural: the human is the only unbounded source of exogenous
signal, and criteria formation is logically prior to criteria application.

**What would falsify this.** A domain with no formal correctness oracle, where
self-generated data improves a model across many generations with no human signal
at any point. That experiment does not appear in this corpus. Absolute Zero is the
closest thing to it and it explicitly relies on a code executor for ground truth.

**Which single source, if withdrawn, changes the answer.** `s-018`. The
knowledge-centre bound is the only formal support for "a model verifier is not
enough," and it is one T3 preprint working at small scale.

---

## Gaps

**Checked and absent.**

- No peer-reviewed cost-per-label breakdown for expert curation. Searched; the
  available material is vendor pricing (T4, not registered).
- No T1 source anywhere in the corpus. There is no systematic review with a
  registered protocol on this question. The report must not imply meta-analytic
  support for anything.
- No evidence found that a layered LLM-annotator pipeline is "standard" practice
  (`c-034`, failed). That is an empirical claim about industry adoption and would
  need a practitioner survey.
- No source supporting production-trace golden datasets over synthetic test cases
  (`c-033`, failed). The nearest captured source argues the opposite direction.

**Not checked — out of scope by the brief.**

- Copyright, licensing and the legality of training-data acquisition.
- Privacy regulation mechanics. This one bit: the inherited claim that synthetic
  data wins in health, legal and finance was dropped rather than assessed, because
  the brief excluded the area. If the paper wants that section, it needs its own
  gathering pass.
- Modalities other than text, except where cited across.
- Data-market economics. No source on what curated data actually sells for.

**Not checked — ran out of road.**

- Aroyo and Welty (2015), the standard theory source for annotator disagreement as
  signal rather than noise, was sought and could not be retrieved (Wiley 403, AAAI
  mirror 404). It is not registered and not cited. Its absence weakens sq3's
  theoretical framing, and a library copy would strengthen the paper.

**Unknowable from public sources.**

- What frontier labs actually spend on human data, and the ratio of synthetic to
  human data in current frontier training mixes. `c-020` is the closest public
  figure and it is three years old and self-reported.

## Methodological limitation

The `claim-auditor` agent was not dispatched — this session runs under an
instruction not to spawn agents unless asked. Gate rule G7 does not require it
here, because every binding uses a quote locator rather than a section or table
locator. Load-bearing claims were audited instead by re-reading the surrounding
passage in the snapshot, which is how the `c-036`/`c-037` reversal was caught. That
is a weaker check than a fresh-context auditor that never sees the narrative, and
the report inherits that limitation.
