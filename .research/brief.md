# Research brief: Data use in the AI age — the curation constraint

## Question

Given that machine-generated data is abundant while human-curated data is scarce
and costly, what division of labour between the two is actually supported by
evidence — and what specifically makes human curation expensive enough to remain
the binding constraint?

## Decision this feeds

The central argument of a capstone journal paper. The answer determines whether
the paper argues (a) synthetic data is substituting for human curation and the
constraint is dissolving, (b) synthetic data scales human judgement but cannot
replace it, and curation cost is structural rather than temporary, or (c) the
substitution question is conditional and the conditions are the actual finding.

The user arrives with a prior — abundance without quality, because curation costs
effort, time, process and quality-control standards. That prior is the thing being
tested, not the thing being supported.

## Sub-questions

1. **Recursion.** What happens to models trained on model-generated data, and
   under what conditions does degradation occur or fail to occur? Specifically:
   does the distinction between *replacing* real data and *accumulating* alongside
   it change the outcome, and how strong is the evidence either way?

2. **Where synthetic works.** In which settings does synthetic data demonstrably
   improve outcomes, and what conditions (filtering, verification, a stronger
   generator, a formal correctness signal) does that improvement depend on?

3. **The cost of curation.** What are the documented components of human data
   curation cost — time, money, annotator agreement, process overhead, quality
   control — and is there evidence on which component dominates?

4. **Automated judgement.** How well does LLM-as-judge and LLM annotation agree
   with human judgement, and where does it measurably fail? This bears directly
   on whether the human can be moved out of the loop or only moved later in it.

5. **Scarcity.** Is high-quality human-generated text actually running out on any
   projected timeline, or is the scarcity economic and organisational rather than
   absolute?

Each is answerable without first answering the others. What they mean *together*
is synthesis's job, not gathering's.

## Out of scope

- **Copyright, licensing, and the legality of training-data acquisition.** A large
  live literature with its own methods; it changes what data is *permissible*, not
  what data is *good*, and folding it in would double the paper.
- **Privacy regulation specifics** (GDPR, HIPAA compliance mechanics). Synthetic
  data's privacy motivation is in scope as a *reason people reach for it*; the
  regulatory analysis is not.
- **Modalities other than text**, except where image or tabular evidence is
  decisive on a sub-question. The recursion literature spans modalities and will
  be cited across them; the argument is about language models.
- **Vendor and tool comparison.** No annotation-platform bake-off.
- **Fairness and representational bias as a standalone literature.** Touched only
  where it bears on what "quality" in curation means.
- **Pretraining compute economics.** Adjacent, separately large.

## What a good answer looks like

A conditional claim with the conditions named and sourced — not "synthetic data
works" or "synthetic data collapses models," but the specific circumstances that
separate the two, each bound to a locator that can be opened. Quantities where
quantities exist: agreement rates, cost per label, the number of recursive
generations before measured degradation.

**What would change the prior:** evidence that unfiltered self-generated data at
scale improves models without human anchoring; or evidence that annotation cost is
falling fast enough to stop being the binding constraint; or a demonstration that
LLM judges agree with expert humans closely enough that human review is redundant
rather than merely reduced.

**What would confirm it:** a mechanism for why curation resists automation that
holds across domains, plus evidence that synthetic gains are conditional on a
human-calibrated filter.

## Lens

`academic`, recency window narrowed from the default 10 years to **4 years
(2022-2026)** for the synthetic-data, recursion and LLM-judge literature — this is
a fast-moving computational field where a 2021 result on generative data quality
describes different systems than the ones in question.

**Exception:** the human data-work and annotation-cost literature keeps the full
10-year window. Findings about annotator agreement, labelling process and
organisational incentives are about human process, not model capability, and do
not expire when a model generation turns over.

T1 here means systematic reviews and large pre-registered work; T2 peer-reviewed
primary studies including NeurIPS/ICML/ICLR proceedings; **T3 arXiv preprints,
which is where the frontier of this specific literature genuinely lives** and which
therefore carry real weight in this project, flagged as unreviewed rather than
discounted; T4 press coverage of studies, vendor blog posts, and anything citing a
paper it has not read.

## Known traps

From the lens:

- Citing a paper via another paper's description of it, or via its abstract.
- Reading a press release's framing as the paper's finding.
- A literature that looks unanimous because null results went unpublished.
- Vibe citations: real authors, real venue, a title that does not exist.

Specific to this question:

- **Conflating distillation with recursion.** Training on output from a *stronger*
  model is a different operation from training on your own output. Both get called
  "synthetic data" and the evidence on them points in opposite directions. This is
  the single most likely way to get the paper's central claim wrong.
- **Model collapse overstated from the headline.** The widely-cited Nature result
  concerns a specific *replace-the-data* regime. Whether it generalises to the
  accumulate regime is contested and is sub-question 1, not a settled premise.
- **Benchmark contamination** making synthetic-data gains look larger than they
  are, particularly where the generator and the evaluation share a lineage.
- **Incentive asymmetry in who publishes what.** Annotation vendors publish on the
  irreplaceability of human labelling; frontier labs publish on synthetic
  sufficiency. Neither is disqualifying, both are a reason to check the setup.
- **Inherited claims from the prompt.** The user supplied prior findings including
  an "83% of a 24-person user study" figure and a claim that model collapse is
  "avoidable by accumulating." These enter as leads to verify, not as premises. If
  a locator cannot be opened for one, it is reported as unverified rather than
  quietly dropped.
