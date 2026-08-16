# Abundant and Uncurated: How Data Should Be Used in the AI Age

## Abstract

Data is abundant; high-quality human-curated data is not. This paper asks what
division of labour between machine-generated and human-curated data the evidence
actually supports, and why curation remains expensive. The answer is that machines
should scale the *application* of judgement while humans remain the *source* of the
judgement being applied[^c-106]. Two independent mechanisms produce this
conclusion. A synthetic training loop guided by a model verifier converges on what
that verifier already knows[^c-037], so a closed loop of models redistributes
information rather than creating it. And evaluation criteria cannot be fully
specified before humans have examined outputs[^c-025], so the definition of quality
cannot be delegated in advance. The conclusion is contested: at least one system
has reached state-of-the-art reasoning performance with no human-curated data at
all[^c-015], and that result is addressed directly rather than set aside.

---

## 1. The answer, and what it is not

The popular framing holds that human judgement is qualitatively better than machine
judgement and therefore irreplaceable. The evidence does not support that framing.
In a peer-reviewed comparison, ChatGPT's zero-shot annotation accuracy exceeded
that of crowd workers by roughly 25 percentage points on average[^c-027], at a cost
below $0.003 per annotation — about thirty times cheaper than the human
alternative[^c-028]. Strong model judges agree with human preferences at rates above
80 per cent, matching the rate at which humans agree with each other[^c-023]. Any
argument for the human that rests on comparative accuracy has to get past these
numbers, and most such arguments do not.

The argument that does survive is not about accuracy. It is informational and
structural, and it is set out in sections 3 and 6.

---

## 2. Model collapse describes a regime, not a fact about synthetic data

The most-cited result in this area is that indiscriminately training generative
models on data produced by other models causes model collapse, in which models
progressively forget the true underlying data distribution even when that
distribution is not itself changing[^c-001]. A characteristic symptom is that the
tails of the original content distribution disappear[^c-002].

**The sources disagree about how far this generalises, and the disagreement is the
most useful thing in this section.** The peer-reviewed result reports degradation
without qualifying it by training regime[^c-001]. Later work qualifies it heavily:
when each generation's real data is *replaced* by synthetic data, test error rises
with each iteration[^c-003], but when synthetic data *accumulates* alongside the
original real data, collapse is avoided[^c-004]. A position paper adds that the
literature is arguing about eight different definitions of degradation rather than
one[^c-005], and that the replace paradigm drives the proportion of real data to
zero immediately after the first iteration[^c-006] — a condition that describes no
real training pipeline.

These are not contradictory findings. They are findings about different setups, and
the later work adds an arm the earlier work did not run. Two observations follow.

First, a tier inversion that a reader weighting by venue would get backwards: the
peer-reviewed source carries the *less* qualified claim and the preprints carry the
more careful one[^c-100]. In a fast-moving computational field, recency can
outweigh review status, and citing only the peer-reviewed framing produces a more
alarming account than the literature supports.

Second, the correction status is clean. The Nature paper carries a 2025 Author
Correction amending text in its Theoretical intuition section[^c-007]; it is a
symbol substitution, not a retraction, and it does not disturb the findings. This is
recorded because a heavily cited paper with a correction attracts the assumption
that the correction was substantive.

---

## 3. The mechanism: exogenous signal, and the limit of a model verifier

Underneath the regime distinction sits a mechanism that generalises better than
either result.

Continual improvement requires that data be curated in a way that injects signal
*exogenous to the system that produced the original data*[^c-009]. Without such
curation, performance can plateau or collapse after many iterations[^c-008]. Note
what this specifies: exogenous signal, not human signal.

This distinction appears at first to dissolve the case for the human. A verifier
"whether a human or a better model" is sufficient to prevent collapse[^c-010] —
which reads as though a stronger model substitutes cleanly for a person.

It does not, and the qualification is decisive. Where a model rather than a human
supplies verification, early gains plateau and may reverse unless that verifier is
perfectly reliable[^c-036]. More fundamentally, verifier-guided retraining
ultimately drives the parameter estimate towards the verifier's own knowledge
centre[^c-037]. A model verifier does not add information to the system; it
transfers information the verifier already holds, and the process then terminates.

This is the paper's central mechanism, and it should be read with its limits
visible. It rests on a single preprint whose long-run analysis is theoretical, and
it has not been demonstrated at frontier scale[^c-101]. If that source fails to
replicate, this argument weakens from a formal result to a plausibility claim. It is
simultaneously the most important and the least corroborated element of the case
assembled here.

---

## 4. Where synthetic data earns its place

Synthetic data improves models conditionally rather than generally, and the binding
condition is the strength of verification applied to it rather than the volume
generated[^c-102]. This conclusion is held at low confidence, for reasons given
below.

Filtering enhances learning **only** when the underlying verification is strong
enough to supply a high-resolution correctness signal[^c-011]. The corollary is
routinely omitted from practitioner accounts: naive or rigid verification filtering
has been observed to produce no improvement at all[^c-012]. A judge filter is not
automatically valuable. Weak filtering is decorative, and over-strict filtering
removes the diversity that measurably correlates with both pre-training and
supervised fine-tuning performance[^c-013]. Relatedly, the quality of the seed data
fed to a generator matters more to downstream performance than whether the
generated knowledge is novel[^c-014] — which relocates the problem rather than
solving it, since seed quality is itself a curation output.

One setting where synthetic data does hold up on its own terms is the calibration of
evaluation criteria. Synthetic test data has been found as effective as hand-crafted
data both for refining evaluation criteria and for aligning with user
expectations[^c-029]. The finding is worth stating precisely, because it is
routinely over-read. It concerns the refinement of *judge criteria*, not the quality
of training data, and it rests on a preprint with 24 participants. The
frequently-quoted companion figure — that 83 per cent of those participants
preferred the synthetic-generation tool to creating or selecting test cases by
hand[^c-030] — measures perceived workload and tool preference, not data quality or
model outcomes. It is evidence that people would rather not hand-write test cases.
That is a real finding about the economics of curation effort, and it is not
evidence that synthetic data is good.

Two limits on this section. The strongest filtering evidence comes from the code
domain, where a compiler supplies ground truth for free — the setting most
favourable to automated verification and least representative of tone, safety or
domain nuance. And the seed-quality finding is vendor-authored by a company selling
data curation, whose commercial interest points the same way as its result[^c-102].
Confidence is set by the weakest link in that chain, not by the average.

### The strongest case against this paper

One system trained by self-play with no human-curated data outperformed models
trained on expert-curated human data in the coding category[^c-015]. This is real,
it is a spotlight result, and it is the most serious challenge to the argument
advanced here[^c-106].

Three considerations bound it, none of which dismisses it. The measured margin is
0.3 absolute percentage points[^c-035] — a near-tie rather than a rout, and one
that the abstract-level framing obscures. The approach depends on a code executor
supplying validation and verifiable feedback[^c-016], which exists for code and
mathematics and does not exist for judgements about tone or appropriateness. And a
falsifying experiment has not been run: a domain with no formal correctness oracle,
in which self-generated data improves a model across many generations with no human
signal at any point[^c-106].

---

## 5. Why curation stays expensive

Human curation is costly for structural rather than temporary reasons: the volume
required is continuous rather than one-off, the failures it prevents are delayed
and hard to detect, and the process encodes contested judgement rather than
recording facts[^c-103].

**Volume is continuous.** A frontier alignment pipeline collected human preference
data on a weekly basis, comprising over one million binary model-generation
comparisons[^c-020]. This is a standing operation, not a dataset assembled once.

**Failure is invisible until late.** Data cascades — compounding downstream failures
originating in data problems — are opaque and delayed, with poor indicators and
metrics for detecting them[^c-019]; 92 per cent of the AI practitioners surveyed
reported experiencing at least one[^c-017]. This is the load-bearing explanation for
why curation resists automation. A process whose defects surface only downstream
offers no contemporaneous quality signal to automate against. The feedback loop that
cheap automated QA would require does not exist at the time the work is done.

**Curation is normative, not clerical.** Annotation instruction documents reproduce
and normalise the worldviews of the parties commissioning the data[^c-022].
Curation is not transcription that a cheaper worker could perform equally well; it
encodes a position on what the right answer is. This is why quality standards are
expensive to write and contested to apply. It is also why the cost has largely been
*displaced* rather than removed: data workers producing training data are paid as
little as a few cents per task and typically lack the social protections attached
to employment[^c-021]. That figure comes from fieldwork in Venezuela and Argentina
and should not be generalised to expert annotation in high-income markets.

Finally, the discipline's own account of itself is that data is the most
under-valued and de-glamorised aspect of AI practice[^c-018] — a characterisation
by the authors rather than a measurement, but a widely echoed one.

**A gap in this section.** No peer-reviewed cost-per-label figure for *expert*
curation was found. The available cost comparison uses crowd workers on
classification tasks as the human baseline[^c-028], which is not the expert
judgement this section concerns. This is the thinnest part of the evidence assembled
here.

---

## 6. What automation can take over, and what it cannot

Automated judgement can substitute for the graded labour of *applying* criteria, but
not for the *formation* of criteria[^c-104]. The sources genuinely disagree here,
and the disagreement is presented before the reconciliation.

Against the human: model judges match human-human agreement rates[^c-023]; models
beat crowd workers substantially on accuracy[^c-027] and overwhelmingly on
cost[^c-028].

For the human: it is impossible to completely determine evaluation criteria prior to
human judging of model outputs[^c-025]. The circularity has a name — criteria drift:
users need criteria in order to grade outputs, and grading outputs is what allows
them to define the criteria[^c-026]. The obvious objection — grade first, then
specify — was tested and does not hold: participants who graded before specifying
criteria still refined those criteria on further grading[^c-038].

**The reconciliation is a distinction of kind, not degree.** Every result favouring
automation measures performance against a *fixed rubric*. The rubric is precisely
the artefact that cannot be fixed in advance[^c-025]. This is a structural argument
rather than a capability argument: it does not claim models are not yet good enough
at judging, but that the specification of what counts as good cannot be completed
before the examining happens. A more capable model makes the applying cheaper; it
does not remove the prior step. The conclusion would fall if someone demonstrated
stable criteria formation without human grading[^c-104].

One caution on citation practice. The paper reporting agreement above 80 per
cent[^c-023] is the same paper documenting that model judges exhibit position bias,
verbosity bias, self-enhancement bias and limited reasoning ability[^c-024]. The
headline figure and the failure taxonomy come from one source and should always
travel together.

---

## 7. Is high-quality human data actually running out?

The shortage is partly a forecast about absolute supply and partly an observed
withdrawal of access, and only the second is currently measurable[^c-105].

The forecast: if current trends continue, models will be trained on datasets roughly
equal in size to the stock of public human text data between 2026 and 2032, or
slightly earlier if models are overtrained[^c-031]. This is a projection, not an
observation, and its authors are an organisation whose profile depends on scaling
forecasts.

The measurement: more than 28 per cent of the most actively maintained, critical
sources in the C4 corpus have become fully restricted through robots.txt[^c-032].

These are different phenomena and should not be blended. Exhaustion is a supply
problem that better curation could in principle address. Consent withdrawal is a
governance problem that curation effort cannot touch, because the data still exists
and is merely no longer permitted. A significant part of the scarcity in "abundant
but uncurated" is therefore not scarcity of text at all — it is scarcity of
permission[^c-105].

---

## 8. Conclusion

The proposition that data is abundant while high-quality curated data is scarce is
correct, and the reasons are more structural than the usual account of effort and
process suggests. Curation is expensive because its failures are undetectable at the
time of the work[^c-019] and because it encodes contested judgement rather than
recording facts[^c-022] — neither of which is fixed by better tooling.

The corresponding prescription is narrower than "keep humans in the loop." Machines
should absorb the application of judgement at scale, where they are demonstrably
accurate and radically cheaper[^c-027][^c-028]. Humans should own two things that
cannot be delegated: the formation of the criteria, because criteria cannot be
specified before outputs are examined[^c-025]; and the supply of exogenous signal,
because a loop verified by models converges on what those models already
know[^c-037].

That conclusion is held at moderate confidence and it is contested[^c-106]. The
strongest counter-evidence — state-of-the-art reasoning learned with no human data —
is real[^c-015], and its scope condition, a code executor providing ground
truth[^c-016], is exactly the condition that does not hold in the domains where
curation is hardest.

---

## 9. Limitations

**Evidence base.** 23 distinct works, 12 at T2 (peer-reviewed) and 15 at T3
(preprints and conference papers). **There is no T1 source**: no systematic review
with a registered protocol exists on this question, and nothing here should be read
as carrying meta-analytic support.

**Single-source dependency.** The knowledge-centre bound[^c-037] — the formal basis
for claiming a model verifier is insufficient — rests on one T3 preprint whose
long-run results are theoretical and demonstrated at small scale[^c-101]. It is the
most load-bearing and least corroborated claim in this paper.

**Contested conclusions.** Three of the seven conclusions are formally
mixed-stance[^c-100][^c-104][^c-106], meaning the underlying sources disagree. Each
is presented above with the disagreement rather than a chosen side.

**Domain skew.** The strongest evidence on verification comes from code, where
ground truth is free[^c-102]. Generalisation to tone, safety and domain nuance is an
inference this evidence supports directionally but does not establish.

**Out of scope by design.** Copyright and licensing; privacy regulation mechanics;
non-text modalities; data-market economics. The frequently repeated claim that
synthetic data wins decisively in privacy-sensitive domains such as health and
finance was *not assessed here* — it falls in the excluded area and would require
its own gathering pass. It should not be inferred from this paper.

**Unretrieved source.** Aroyo and Welty (2015), the standard theoretical treatment
of annotator disagreement as signal rather than noise, could not be obtained
(publisher paywall; mirror unavailable). It is not cited, and section 5's
theoretical framing is weaker for its absence.

**Unknowable from public sources.** What frontier labs currently spend on human data,
and the present ratio of synthetic to human data in frontier training mixes. The
closest public figure[^c-020] is self-reported and three years old.

**Two claims were rejected in verification** and appear nowhere above: that golden
datasets built from production traces outperform synthetic test cases, and that a
layered LLM-annotator/judge/human-review pipeline is now standard practice. Neither
could be established from any captured source, and the first is contradicted by the
nearest source to it.

## References

[^c-106]: The defensible division of labour is that machines scale the application of judgement while humans remain the source of the judgement being applied, because a synthetic loop converges on what its verifier already knows and evaluation criteria cannot be fully specified before outputs are seen.
    — *Who Validates the Validators? Aligning LLM-Assisted Evaluation of LLM Outputs with Human Preferences (arXiv full text)*, ACM UIST 2024 / arXiv (Shankar, Zamfirescu-Pereira, Hartmann, Parameswaran, Arawjo), 2024-04-18. <https://arxiv.org/html/2404.12272v1> (accessed 2026-08-16) [T2]
      *Escaping Model Collapse via Synthetic Data Verification: Near-term Improvements and Long-term Convergence*, arXiv, 2025-10-19. <https://arxiv.org/html/2510.16657v2> (accessed 2026-08-16) [T3]
      *Escaping Collapse: The Strength of Weak Data for Large Language Model Training*, arXiv, 2025-02-13. <https://arxiv.org/html/2502.08924> (accessed 2026-08-16) [T3]
    Stance: MIXED — sources disagree; see s-019. Synthesised conclusion; rests on c-101, c-104, c-025, c-037.

[^c-037]: Verifier-guided retraining ultimately drives the parameter estimate towards the verifier's own knowledge centre.
    — *Escaping Model Collapse via Synthetic Data Verification: Near-term Improvements and Long-term Convergence*, arXiv, 2025-10-19. <https://arxiv.org/html/2510.16657v2> (accessed 2026-08-16) [T3]

[^c-025]: It is impossible to completely determine evaluation criteria prior to humans judging LLM outputs, because grading outputs is itself what allows the criteria to be defined.
    — *Who Validates the Validators? Aligning LLM-Assisted Evaluation of LLM Outputs with Human Preferences (arXiv full text)*, ACM UIST 2024 / arXiv (Shankar, Zamfirescu-Pereira, Hartmann, Parameswaran, Arawjo), 2024-04-18. <https://arxiv.org/html/2404.12272v1> (accessed 2026-08-16) [T2]

[^c-015]: A self-play system trained without any human-curated data outperformed models trained with expert-curated human data in the coding category.
    — *Absolute Zero: Reinforced Self-play Reasoning with Zero Data*, arXiv / NeurIPS 2025 spotlight (Zhao et al., LeapLab THU), 2025-05-06. <https://arxiv.org/html/2505.03335> (accessed 2026-08-16) [T3]

[^c-027]: ChatGPT's zero-shot annotation accuracy exceeded that of crowd workers by about 25 percentage points on average across four datasets of tweets and news articles.
    — *ChatGPT outperforms crowd-workers for text-annotation tasks*, PNAS 120(30) / arXiv preprint version (Gilardi, Alizadeh, Kubli), 2023-03-27. <https://arxiv.org/pdf/2303.15056> (accessed 2026-08-16) [T2]

[^c-028]: Per-annotation cost using ChatGPT was less than $0.003, about thirty times cheaper than MTurk.
    — *ChatGPT outperforms crowd-workers for text-annotation tasks*, PNAS 120(30) / arXiv preprint version (Gilardi, Alizadeh, Kubli), 2023-03-27. <https://arxiv.org/pdf/2303.15056> (accessed 2026-08-16) [T2]

[^c-023]: Strong LLM judges reach an agreement rate with human preferences exceeding 80 per cent, the same level as human-human agreement.
    — *Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena (full text v4)*, NeurIPS 2023 D&B (Zheng, Chiang, Sheng et al.), 2023-06-09. <https://arxiv.org/html/2306.05685v4> (accessed 2026-08-16) [T2]

[^c-001]: Indiscriminately training generative models on data produced by other models causes model collapse, in which models progressively forget the true underlying data distribution even when that distribution is not itself changing.
    — *AI models collapse when trained on recursively generated data*, Nature (Shumailov, Shumaylov, Zhao, Papernot, Anderson, Gal), 2024-07-24. <https://www.nature.com/articles/s41586-024-07566-y> (accessed 2026-08-16) [T2]

[^c-002]: A specific consequence of model collapse is that the tails of the original content distribution disappear.
    — *AI models collapse when trained on recursively generated data*, Nature (Shumailov, Shumaylov, Zhao, Papernot, Anderson, Gal), 2024-07-24. <https://www.nature.com/articles/s41586-024-07566-y> (accessed 2026-08-16) [T2]

[^c-003]: When each generation's real data is replaced by synthetic data, test error increases with the number of model-fitting iterations.
    — *Is Model Collapse Inevitable? Breaking the Curse of Recursion by Accumulating Real and Synthetic Data (full text v2)*, arXiv (Gerstgrasser, Schaeffer, Dey, Rafailov et al.), 2024-04-01. <https://arxiv.org/html/2404.01413v2> (accessed 2026-08-16) [T3]

[^c-004]: Accumulating successive generations of synthetic data alongside the original real data avoids model collapse.
    — *Is Model Collapse Inevitable? Breaking the Curse of Recursion by Accumulating Real and Synthetic Data (full text v2)*, arXiv (Gerstgrasser, Schaeffer, Dey, Rafailov et al.), 2024-04-01. <https://arxiv.org/html/2404.01413v2> (accessed 2026-08-16) [T3]

[^c-005]: The published model-collapse literature operates with eight different definitions of performance degradation rather than one agreed definition.
    — *Position: Model Collapse Does Not Mean What You Think*, arXiv (Schaeffer et al.), 2025-03-05. <https://arxiv.org/html/2503.03150> (accessed 2026-08-16) [T3]

[^c-006]: Under the replace paradigm the proportion of real data in the training corpus becomes zero immediately after the first iteration, which is why that paradigm is a poor model of real-world training practice.
    — *Position: Model Collapse Does Not Mean What You Think*, arXiv (Schaeffer et al.), 2025-03-05. <https://arxiv.org/html/2503.03150> (accessed 2026-08-16) [T3]

[^c-100]: Recursive training degrades models under the regime where synthetic data replaces real data, and not under the regime where it accumulates alongside it; the widely repeated claim that training on model output causes collapse is therefore true of a setup that does not describe how models are actually trained.
    — *Is Model Collapse Inevitable? Breaking the Curse of Recursion by Accumulating Real and Synthetic Data (full text v2)*, arXiv (Gerstgrasser, Schaeffer, Dey, Rafailov et al.), 2024-04-01. <https://arxiv.org/html/2404.01413v2> (accessed 2026-08-16) [T3]
      *Position: Model Collapse Does Not Mean What You Think*, arXiv (Schaeffer et al.), 2025-03-05. <https://arxiv.org/html/2503.03150> (accessed 2026-08-16) [T3]
    Stance: MIXED — sources disagree; see s-001. Synthesised conclusion; rests on c-001, c-003, c-004, c-005, c-006.

[^c-007]: The 2025 Author Correction to the Nature model-collapse paper amends text in the paper's Theoretical intuition section.
    — *Author Correction: AI models collapse when trained on recursively generated data*, Nature, 2025. <https://www.nature.com/articles/s41586-025-08905-3> (accessed 2026-08-16) [T2]

[^c-009]: Preventing degradation in recursive training requires curation that injects signal exogenous to the system that produced the original data.
    — *Escaping Collapse: The Strength of Weak Data for Large Language Model Training*, arXiv, 2025-02-13. <https://arxiv.org/html/2502.08924> (accessed 2026-08-16) [T3]

[^c-008]: Without curation, LLM performance can plateau or collapse after many training iterations.
    — *Escaping Collapse: The Strength of Weak Data for Large Language Model Training*, arXiv, 2025-02-13. <https://arxiv.org/html/2502.08924> (accessed 2026-08-16) [T3]

[^c-010]: The exogenous signal that prevents collapse can be supplied by a better model rather than by a human.
    — *Escaping Model Collapse via Synthetic Data Verification: Near-term Improvements and Long-term Convergence*, arXiv, 2025-10-19. <https://arxiv.org/html/2510.16657v2> (accessed 2026-08-16) [T3]

[^c-036]: Where a model rather than a human supplies the verification signal, early gains plateau and may reverse unless that verifier is perfectly reliable.
    — *Escaping Model Collapse via Synthetic Data Verification: Near-term Improvements and Long-term Convergence*, arXiv, 2025-10-19. <https://arxiv.org/html/2510.16657v2> (accessed 2026-08-16) [T3]

[^c-101]: What prevents degradation is signal exogenous to the system that produced the data; a stronger model can supply it, but only up to that model's own knowledge, which makes human signal the only source not bounded by an existing model.
    — *Escaping Collapse: The Strength of Weak Data for Large Language Model Training*, arXiv, 2025-02-13. <https://arxiv.org/html/2502.08924> (accessed 2026-08-16) [T3]
      *Escaping Model Collapse via Synthetic Data Verification: Near-term Improvements and Long-term Convergence*, arXiv, 2025-10-19. <https://arxiv.org/html/2510.16657v2> (accessed 2026-08-16) [T3]
    Synthesised conclusion; rests on c-009, c-010, c-036, c-037.

[^c-102]: Synthetic data improves models conditionally rather than generally, and the binding condition is the strength of the verification applied to it, not the volume generated.
    — *Verification Limits Code LLM Training*, arXiv, 2025-09-25. <https://arxiv.org/html/2509.20837> (accessed 2026-08-16) [T3]
      *BeyondWeb: Lessons from Scaling Synthetic Data for Trillion-scale Pretraining*, arXiv / DatologyAI, 2025-08-14. <https://arxiv.org/html/2508.10975> (accessed 2026-08-16) [T3]
    Confidence: LOW. Synthesised conclusion; rests on c-011, c-012, c-013, c-014.

[^c-011]: Filtering synthetic data improves learning only when the underlying verification is strong enough to provide a high-resolution correctness signal.
    — *Verification Limits Code LLM Training*, arXiv, 2025-09-25. <https://arxiv.org/html/2509.20837> (accessed 2026-08-16) [T3]

[^c-012]: Verification-based filtering of synthetic data can produce no improvement at all when applied naively or rigidly.
    — *Verification Limits Code LLM Training*, arXiv, 2025-09-25. <https://arxiv.org/html/2509.20837> (accessed 2026-08-16) [T3]

[^c-013]: Measured diversity of synthetic data correlates positively with both pre-training and supervised fine-tuning performance.
    — *On the Diversity of Synthetic Data and its Impact on Training Large Language Models*, arXiv, 2024-10-19. <https://arxiv.org/html/2410.15226> (accessed 2026-08-16) [T3]

[^c-014]: The quality of the seed data used for synthetic generation matters more to downstream performance than ensuring the generated knowledge is novel.
    — *BeyondWeb: Lessons from Scaling Synthetic Data for Trillion-scale Pretraining*, arXiv / DatologyAI, 2025-08-14. <https://arxiv.org/html/2508.10975> (accessed 2026-08-16) [T3]
    Confidence: LOW.

[^c-029]: Synthetic test data proved as effective as hand-crafted data for refining evaluation criteria and aligning with user expectations.
    — *Generate, Evaluate, Iterate: Synthetic Data for Human-in-the-Loop Refinement of LLM Judges*, arXiv (HCI/eval), 2025-11-06. <https://arxiv.org/html/2511.04478v1> (accessed 2026-08-16) [T3]
    Confidence: LOW.

[^c-030]: In a study with 24 participants, 83 per cent preferred a synthetic data generation tool over manually creating or selecting test cases.
    — *Generate, Evaluate, Iterate: Synthetic Data for Human-in-the-Loop Refinement of LLM Judges*, arXiv (HCI/eval), 2025-11-06. <https://arxiv.org/html/2511.04478v1> (accessed 2026-08-16) [T3]
    Confidence: LOW.

[^c-035]: The margin by which that zero-human-data self-play system beat expert-curated human data in the coding category was 0.3 absolute percentage points.
    — *Absolute Zero: Reinforced Self-play Reasoning with Zero Data*, arXiv / NeurIPS 2025 spotlight (Zhao et al., LeapLab THU), 2025-05-06. <https://arxiv.org/html/2505.03335> (accessed 2026-08-16) [T3]

[^c-016]: That zero-human-data self-play result depends on a code executor supplying validation and verifiable feedback, which bounds the domains in which the approach can work.
    — *Absolute Zero: Reinforced Self-play Reasoning with Zero Data*, arXiv / NeurIPS 2025 spotlight (Zhao et al., LeapLab THU), 2025-05-06. <https://arxiv.org/html/2505.03335> (accessed 2026-08-16) [T3]

[^c-103]: Human curation is costly for structural reasons rather than temporary ones: the volume required is continuous rather than one-off, the failures it prevents are delayed and hard to detect, and the process encodes contested judgement rather than recording facts.
    — *Llama 2: Open Foundation and Fine-Tuned Chat Models (full text)*, arXiv / Meta AI (Touvron et al.), 2023-07-18. <https://arxiv.org/pdf/2307.09288> (accessed 2026-08-16) [T3]
      *"Everyone wants to do the model work, not the data work": Data Cascades in High-Stakes AI*, ACM CHI 2021 (Sambasivan, Kapania, Highfill, Akrong, Paritosh, Aroyo), 2021-05-07. <https://dl.acm.org/doi/10.1145/3411764.3445518> (accessed 2026-08-16) [T2]
      *The Data-Production Dispositif (full text)*, ACM CSCW 2022 / arXiv (Miceli, Posada), 2022-05-24. <https://arxiv.org/pdf/2205.11963> (accessed 2026-08-16) [T2]
    Synthesised conclusion; rests on c-017, c-019, c-020, c-021, c-022.

[^c-020]: A frontier alignment pipeline collected human preference data on a weekly basis consisting of over one million binary model-generation comparisons.
    — *Llama 2: Open Foundation and Fine-Tuned Chat Models (full text)*, arXiv / Meta AI (Touvron et al.), 2023-07-18. <https://arxiv.org/pdf/2307.09288> (accessed 2026-08-16) [T3]

[^c-019]: Data cascades are opaque and delayed, with poor indicators and metrics for detecting them.
    — *"Everyone wants to do the model work, not the data work": Data Cascades in High-Stakes AI*, ACM CHI 2021 (Sambasivan, Kapania, Highfill, Akrong, Paritosh, Aroyo), 2021-05-07. <https://dl.acm.org/doi/10.1145/3411764.3445518> (accessed 2026-08-16) [T2]

[^c-017]: 92 per cent of AI practitioners surveyed reported experiencing one or more data cascades.
    — *"Everyone wants to do the model work, not the data work": Data Cascades in High-Stakes AI*, ACM CHI 2021 (Sambasivan, Kapania, Highfill, Akrong, Paritosh, Aroyo), 2021-05-07. <https://dl.acm.org/doi/10.1145/3411764.3445518> (accessed 2026-08-16) [T2]

[^c-022]: Annotation instruction documents reproduce and normalise the worldviews of the parties commissioning the data.
    — *The Data-Production Dispositif (full text)*, ACM CSCW 2022 / arXiv (Miceli, Posada), 2022-05-24. <https://arxiv.org/pdf/2205.11963> (accessed 2026-08-16) [T2]

[^c-021]: Data workers producing machine-learning training data are paid as little as a few cents per task and typically lack the social protections tied to employment relations.
    — *The Data-Production Dispositif (full text)*, ACM CSCW 2022 / arXiv (Miceli, Posada), 2022-05-24. <https://arxiv.org/pdf/2205.11963> (accessed 2026-08-16) [T2]

[^c-018]: Data is the most under-valued and de-glamorised aspect of AI practice.
    — *"Everyone wants to do the model work, not the data work": Data Cascades in High-Stakes AI*, ACM CHI 2021 (Sambasivan, Kapania, Highfill, Akrong, Paritosh, Aroyo), 2021-05-07. <https://dl.acm.org/doi/10.1145/3411764.3445518> (accessed 2026-08-16) [T2]

[^c-104]: Automated judgement can substitute for the graded labour of applying criteria but not for the formation of criteria, because criteria cannot be fully specified before humans have looked at outputs.
    — *Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena (full text v4)*, NeurIPS 2023 D&B (Zheng, Chiang, Sheng et al.), 2023-06-09. <https://arxiv.org/html/2306.05685v4> (accessed 2026-08-16) [T2]
      *ChatGPT outperforms crowd-workers for text-annotation tasks*, PNAS 120(30) / arXiv preprint version (Gilardi, Alizadeh, Kubli), 2023-03-27. <https://arxiv.org/pdf/2303.15056> (accessed 2026-08-16) [T2]
      *Who Validates the Validators? Aligning LLM-Assisted Evaluation of LLM Outputs with Human Preferences (arXiv full text)*, ACM UIST 2024 / arXiv (Shankar, Zamfirescu-Pereira, Hartmann, Parameswaran, Arawjo), 2024-04-18. <https://arxiv.org/html/2404.12272v1> (accessed 2026-08-16) [T2]
    Stance: MIXED — sources disagree; see s-013, s-027. Synthesised conclusion; rests on c-023, c-024, c-025, c-026, c-027, c-028.

[^c-026]: Criteria drift names the circular dependency in which users need criteria to grade outputs but need to grade outputs in order to define criteria.
    — *Who Validates the Validators? Aligning LLM-Assisted Evaluation of LLM Outputs with Human Preferences (arXiv full text)*, ACM UIST 2024 / arXiv (Shankar, Zamfirescu-Pereira, Hartmann, Parameswaran, Arawjo), 2024-04-18. <https://arxiv.org/html/2404.12272v1> (accessed 2026-08-16) [T2]

[^c-038]: Participants who graded outputs before specifying criteria still refined those criteria upon further grading.
    — *Who Validates the Validators? Aligning LLM-Assisted Evaluation of LLM Outputs with Human Preferences (arXiv full text)*, ACM UIST 2024 / arXiv (Shankar, Zamfirescu-Pereira, Hartmann, Parameswaran, Arawjo), 2024-04-18. <https://arxiv.org/html/2404.12272v1> (accessed 2026-08-16) [T2]

[^c-024]: LLM judges exhibit position bias, verbosity bias, self-enhancement bias and limited reasoning ability.
    — *Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena (full text v4)*, NeurIPS 2023 D&B (Zheng, Chiang, Sheng et al.), 2023-06-09. <https://arxiv.org/html/2306.05685v4> (accessed 2026-08-16) [T2]

[^c-105]: The shortage of high-quality human data is partly a forecast about absolute supply and partly an observed withdrawal of access, and the second is already measurable while the first is not yet.
    — *Position: Will we run out of data? Limits of LLM scaling based on human-generated data (full text v2)*, ICML 2024 / arXiv (Villalobos, Ho, Sevilla, Besiroglu, Heim, Hobbhahn), 2024-06-04. <https://arxiv.org/pdf/2211.04325> (accessed 2026-08-16) [T2]
      *Consent in Crisis: The Rapid Decline of the AI Data Commons*, Data Provenance Initiative, MIT (Longpre et al.); NeurIPS 2024 D&B, 2024-07-20. <https://arxiv.org/html/2407.14933> (accessed 2026-08-16) [T2]
    Synthesised conclusion; rests on c-031, c-032.

[^c-031]: If current trends continue, models will be trained on datasets roughly equal in size to the available stock of public human text data between 2026 and 2032, or slightly earlier if models are overtrained.
    — *Position: Will we run out of data? Limits of LLM scaling based on human-generated data (full text v2)*, ICML 2024 / arXiv (Villalobos, Ho, Sevilla, Besiroglu, Heim, Hobbhahn), 2024-06-04. <https://arxiv.org/pdf/2211.04325> (accessed 2026-08-16) [T2]

[^c-032]: More than 28 per cent of the most actively maintained, critical sources in the C4 corpus have become fully restricted from use through robots.txt.
    — *Consent in Crisis: The Rapid Decline of the AI Data Commons*, Data Provenance Initiative, MIT (Longpre et al.); NeurIPS 2024 D&B, 2024-07-20. <https://arxiv.org/html/2407.14933> (accessed 2026-08-16) [T2]

