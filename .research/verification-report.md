# Verification report

**Verdict: PASS**

| | |
|---|---|
| Report | `.research/report.md` |
| Sources in ledger | 27 |
| Claims in ledger | 45 |
| Claims cited by the report | 43 |
| Hard failures | 0 |
| Warnings | 17 |

## Hard failures

None. Every cited claim resolves to a ledger row, binds an existing source,
and locates its evidence in a snapshot whose hash still matches.

## Warnings

Advisory. These do not block the report.

### W1 -- Claim in the ledger is never cited

- **claims.jsonl:33** -- claim c-033 is in the ledger but the report never cites it
  Golden datasets built from reviewed production traces reflect real usage in a way synthetic test cases cannot fully replicate.
- **claims.jsonl:34** -- claim c-034 is in the ledger but the report never cites it
  A layered pipeline of LLM annotator, LLM judge, synthetic gap-filling and human review of uncertain cases is now standard practice.

### W2 -- Assertion with no marker

- **report.md:5** -- unbound assertion (asserts something about a named entity)
  Data is abundant; high-quality human-curated data is not.
- **report.md:22** -- unbound assertion (asserts something about a named entity)
  Any argument for the human that rests on comparative accuracy has to get past these numbers, and most such arguments do not.
- **report.md:32** -- unbound assertion (contains a figure)
  It is informational and structural, and it is set out in sections 3 and 6.
- **report.md:75** -- unbound assertion (asserts something about a named entity)
  Underneath the regime distinction sits a mechanism that generalises better than either result.
- **report.md:78** -- unbound assertion (asserts something about a named entity)
  Note what this specifies: exogenous signal, not human signal.
- **report.md:121** -- unbound assertion (contains a figure)
  It concerns the refinement of *judge criteria*, not the quality of training data, and it rests on a preprint with 24 participants.
- **report.md:134** -- unbound assertion (asserts 'strongest')
  The strongest filtering evidence comes from the code domain, where a compiler supplies ground truth for free — the setting most favourabl...
- **report.md:217** -- unbound assertion (asserts something about a named entity)
  **The reconciliation is a distinction of kind, not degree.** Every result favouring automation measures performance against a *fixed rubr...
- **report.md:248** -- unbound assertion (asserts something about a named entity)
  Consent withdrawal is a governance problem that curation effort cannot touch, because the data still exists and is merely no longer permi...
- **report.md:297** -- unbound assertion (asserts something about a named entity)
  Generalisation to tone, safety and domain nuance is an inference this evidence supports directionally but does not establish.
- **report.md:301** -- unbound assertion (asserts something about a named entity)
  **Out of scope by design.** Copyright and licensing; privacy regulation mechanics; non-text modalities; data-market economics.
- **report.md:307** -- unbound assertion (contains a figure)
  It is not cited, and section 5's theoretical framing is weaker for its absence.
- **report.md:312** -- unbound assertion (asserts something about a named entity)
  **Unknowable from public sources.** What frontier labs currently spend on human data, and the present ratio of synthetic to human data in...
- **report.md:316** -- unbound assertion (asserts something about a named entity)
  **Two claims were rejected in verification** and appear nowhere above: that golden datasets built from production traces outperform synth...

### W3 -- Figure in a cited sentence is not in the claim

- **report.md:288** -- the figure 3 does not appear in [^c-037], [^c-101] or its quoted evidence
  **Single-source dependency.** The knowledge-centre bound[^c-037] — the formal basis for claiming a model verifier is insufficient — rests on

---

Rules are defined in `docs/LEDGER-SPEC.md` section 5.
