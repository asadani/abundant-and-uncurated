# Abundant and Uncurated — Summary

*Why synthetic data scales human judgement, and why it cannot become its source.*

**Read the full essay:** [tech.anujsadani.in/abundant-and-uncurated](https://tech.anujsadani.in/abundant-and-uncurated/) ·
**Typeset PDF (24pp):** [ko-fi.com/s/000d383639](https://ko-fi.com/s/000d383639)

---

## The claim most people make, and why it fails

Data is abundant; high-quality curated data is not. The usual defence of human curation
is that human judgement is simply better than machine judgement. It isn't, and the
evidence is not close.

A language model beat crowd workers on annotation accuracy by roughly **25 percentage
points** across four datasets, at under **$0.003 per annotation** — about **thirty times
cheaper** than the human baseline (PNAS 2023).<sup>22</sup> Strong model judges agree with
human preferences **more than 80% of the time**, which is the rate at which humans agree
with each other (NeurIPS 2023).<sup>7</sup>

Any argument for the human that rests on comparative accuracy has already lost. A better
argument exists, and it is not about accuracy at all.

## Model collapse describes a regime, not a fact

The famous result is that training generative models on model-generated data causes
collapse — models forget the true underlying data distribution, and the tails of the
distribution disappear first.<sup>1</sup>

That result travelled stripped of its conditions. Later work shows the outcome flips on a
single variable. When each generation's real data is **replaced** by synthetic data, test
error rises with every iteration. When synthetic data **accumulates** alongside the
original real data, collapse is avoided.<sup>3</sup> A position paper adds that the
literature is arguing about **eight different definitions** of degradation, and that the
replace paradigm drives the proportion of real data to zero after the first iteration —
a condition describing no pipeline anyone operates.<sup>4</sup>

Worth noting: the peer-reviewed paper carries the *less* qualified claim; the preprints
carry the more careful one. Weighting sources by venue gets this backwards.

## The mechanism that actually holds the line

Continual improvement requires curation that injects signal **exogenous to the system
that produced the data**.<sup>11</sup> Note what that specifies — exogenous, not human.

At first this looks like it dissolves the case for people entirely: a verifier "whether a
human or a better model" prevents collapse.<sup>16</sup> Read two sentences further and it
inverts. Where a model supplies verification, gains **plateau and may reverse** unless
that verifier is perfectly reliable, and retraining ultimately **drives the estimate
toward the verifier's own knowledge centre**.<sup>16</sup>

A model verifier does not add information. It transfers information the verifier already
holds, and then the process terminates. The ceiling is informational, not engineering.

> A system that learns only from itself is not learning. It is settling.

## The second mechanism: criteria cannot be pre-specified

It is **impossible to completely determine evaluation criteria prior to human judging of
model outputs**.<sup>8</sup> The circularity has a name — *criteria drift*: you need
criteria to grade outputs, and grading outputs is how you discover the criteria. The
obvious fix, grade first and specify after, was tested and fails: participants who graded
first still revised their criteria on further grading.<sup>8</sup>

This reconciles the disagreement. Every result favouring automation measures performance
**against a fixed rubric** — and the rubric is the artefact that cannot be fixed in
advance. It is a claim about logic, not capability. A better model makes the *applying*
cheaper; it does not remove the step that comes first.

## Why curation stays expensive

Not because tooling is immature. Because of what curation is.

- **Volume is continuous.** One frontier alignment pipeline collected human preference
  data weekly, over **1 million binary comparisons**.<sup>19</sup> A standing operation,
  not a one-off dataset.
- **Failure is invisible until late.** Data cascades are *opaque and delayed, with poor
  indicators and metrics*; **92%** of surveyed practitioners (n=53) hit at least
  one.<sup>13</sup> Automated QA needs a quality signal to optimise against, and a process
  whose defects surface downstream does not emit one at the time of the work.
- **Curation is normative, not clerical.** Annotation instructions *reproduce and
  normalise the worldviews of requesters*.<sup>18</sup> It encodes a position on what the
  right answer is. That is why the cost has been **displaced** rather than removed —
  data workers are paid cents per task, typically without employment protections.<sup>18</sup>

## Where synthetic data genuinely earns its place

Conditionally, and the binding condition is verification strength — not volume. Filtering
helps **only** when verification is strong enough to give a high-resolution correctness
signal, and naive or rigid filtering has produced **no improvement at all**.<sup>10</sup>
Over-strict filtering is actively harmful: it strips the diversity that correlates with
downstream performance.<sup>21</sup>

And synthetic data inherits its quality from curated data — seed quality matters more than
novelty of the generated knowledge.<sup>14</sup> The curation didn't disappear. It moved
upstream.

## The strongest case against this essay

One system trained by self-play with **no human-curated data** outperformed models trained
on expert-curated human data in the coding category.<sup>17</sup> It's a spotlight result
and it deserves to be taken seriously.

Three bounds, none of which dismiss it:

| | |
|---|---|
| **The margin** | **0.3 absolute percentage points**, on one category. A near-tie the abstract framing obscures. |
| **The scope** | It works because a code executor supplies free ground truth. That exists for code and mathematics; not for tone, safety or appropriateness. |
| **The missing test** | A domain with no correctness oracle, where self-generated data improves a model across many generations with no human signal. Not yet run. |

## The scarcity is partly a scarcity of permission

Two different phenomena get blended. The **forecast**: training sets meet the stock of
public human text between **2026 and 2032**.<sup>5</sup> Not yet observed. The
**measurement**: over **28%** of the most actively maintained critical sources in C4 are
now fully restricted via robots.txt.<sup>15</sup> Already happened.

Exhaustion is a supply problem curation could address. Consent withdrawal is a governance
problem it cannot touch — the data still exists and is simply no longer permitted.

## The verdict

**Machines should absorb the application of judgement, where they are demonstrably
accurate and radically cheaper. Humans own two things that cannot be delegated: the
formation of the criteria, and the supply of signal from outside the system.**

Held at moderate confidence, and formally contested. What would falsify it: a domain with
no formal correctness oracle in which self-generated data improves a model across many
generations with no human signal at any point.

---

## On method

Every factual claim in the full essay is bound to an exact quoted passage inside a source
captured to disk and checked by hash. **45 claims, 43 passing and cited, 2 rejected.**
57 quoted bindings, zero mismatches. 22 distinct works — 9 peer-reviewed, 13
preprints/conference papers, no press coverage, and no systematic review with a registered
protocol, so nothing here carries meta-analytic support.

Two widely repeated claims **failed verification** and appear nowhere in the essay:

- *"Golden datasets built from production traces reflect real usage in a way synthetic
  test cases cannot."* The nearest source argues the opposite.
- *"A layered LLM-annotator / judge / synthetic gap-fill / human-review pipeline is now
  standard practice."* No source establishes it.

The ledgers are in [`.research/`](.research/). Full source list with tier labels is in the
[essay's Notes & Sources](https://tech.anujsadani.in/abundant-and-uncurated/).

**Superscripts** above refer to that numbered source list.
