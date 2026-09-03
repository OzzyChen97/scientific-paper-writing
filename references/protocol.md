# Scientific Paper Writing Protocol

This reference preserves the operational content of the source guide. Numerical
targets are defaults to adapt to the actual venue, paper length, deadline, and
available resources. Interpret “recent” relative to the current date rather than
hard-coding the source guide's 2025–2026 window.

## 1. Literature Survey

Input: topic and taxonomy keywords. Output: `references.bib` and
`citation_plan.jsonl`.

### Stage 1: high-recall retrieval

- Run 20–30 keyword queries when the scope warrants it.
- For each taxonomy cell, use at least three query variants: core terms,
  synonyms, and method names.
- Snowball through citation networks from seed papers.
- Original target: 200–500 raw candidates.

### Stage 2: LQS triage

The source guide proposes this literature-quality score:

| Dimension | Weight | Example scoring |
| --- | ---: | --- |
| Recency | 30% | 6 months=10, 1 year=8, 2 years=5, 3 years=3 |
| Citation impact | 25% | citations/month: >=50=10, >=10=8, >=3=6 |
| Venue | 20% | top-tier=10, strong=7, workshop=4 |
| Institution | 10% | top lab=10, top university=9 |
| Acceptance | 15% | accepted=10, under review=5, none=3 |

Original thresholds: LQS >=7.0 is must-cite, 5.0–7.0 is conditional, and <5.0
is dropped. Use these only as prioritization hints. Relevance, methodological
quality, coverage, and direct evidence remain decisive, and low-scoring work may
still be essential.

### Stage 3: citation-depth classification

- A-level: 1–3 paragraphs; section protagonist; 3–5 per chapter.
- B-level: 2–5 sentences; important insight; 5–10 per chapter.
- C-level: one sentence; supporting evidence.
- D-level: not cited.

### Stage 4: venue upgrade and verification

- Cross-check DBLP, OpenReview, publisher pages, or proceedings for acceptance
  status.
- Replace an arXiv-only entry with the accepted version when identity and venue
  are verified.
- Original target: arXiv-only ratio <=60%.
- In batches of about 20 citations, verify title, authors, year, and venue.
- Targets: verification rate >=80%, hallucinated citations=0, papers within one
  year >=40%, accepted papers >=30%.

## 2. Paper Structure and Logic

Input: bibliography and experiment findings. Output: full manuscript sections.

### Survey architecture

1. Introduction: Hook -> Gap -> Contributions -> Roadmap.
2. Background: formal definitions and taxonomy overview.
3. Core chapters: one method family per chapter, with critical assessment.
4. Benchmarks and experiments.
5. Future directions: specific open problems framed as barrier plus attack vector.
6. Conclusion: numbered key findings rather than a repetition of the abstract.

Adapt the exact section count to the venue and argument.

### Paragraph logic patterns

| Pattern | Structure | Use |
| --- | --- | --- |
| Claim–Evidence–Implication | Assert -> Data -> So what | Main body |
| Compare–Contrast | A -> B -> Difference -> Trade-off | Method comparison |
| Concession–Rebuttal | Admit strength -> identify limitation | Critical analysis |
| Funnel | Broad -> Narrow -> This paper | Introduction |

### Taxonomy and claims

- Prefer a multi-axis matrix to a flat list when the literature supports it.
- Aim for mutually exclusive, collectively exhaustive categories, while naming
  boundary cases and overlaps honestly.
- Empty cells can reveal gaps; methods spanning cells can reveal taxonomy tension.
- Prefer `Conjecture` plus `Remark` over `Theorem` when no proof exists.
- Match wording strength to evidence: demonstrates > suggests > may > hypothesize.
- Compare against existing surveys. Recency alone is insufficient differentiation;
  seek a new taxonomy, angle, synthesis, or experiment.

## 3. Experiment Design

Input: a conjecture or gap. Output: `results.json` and
`experiment_summary.md`.

### Design

- State which paper claim the experiment supports or challenges.
- Specify the hypothesis, independent and dependent variables, controls, expected
  results, and statistical analysis before execution.
- Make the test falsifiable, start with the smallest informative pilot, and retain
  a control condition.

### Execute and iterate

The source guide distinguishes a lightweight API path for multi-model comparisons
and prompt ablations from a heavyweight GPU path for training and reward shaping.
Its example scale is 3–5 models by 2–3 conditions by 15–25 tasks by 3 trials.
Choose scale from statistical power, cost, time, and user authorization instead of
assuming this default.

- Ceiling effect: increase difficulty.
- Floor effect: reduce difficulty or investigate implementation errors.
- Non-significant result: reassess power and the hypothesis; do not fish for a
  positive result.
- Surprising result: design a focused follow-up.
- Original stopping rule: at most five iterations, then report the best valid
  result and unresolved limitations.

### Report data before presentation

- `results.json`: configuration, results, statistics, and findings.
- `experiment_summary.md`: purpose, results, and limitations.
- Keep raw data reporting separate from LaTeX tables and figures.

## 4. Academic Figures and Tables

Input: results plus manuscript placeholders. Output: `figures/*` and `tables/*`.

### Tables

Useful types include comparison matrices, benchmark tables, ablation tables,
taxonomy tables, and meta-analysis tables.

- Prefer booktabs-style tables without vertical lines.
- Bold the best result only when “best” is semantically valid and uncertainty does
  not make the distinction misleading.
- Report experimental data as mean ± standard deviation when appropriate.
- Write captions that state the key finding, not merely the contents.

### Figures

- Data-driven plots: matplotlib to vector PDF where practical.
- Architecture and flow diagrams: TikZ or SVG to PDF.
- Simple schematics: raster PNG is acceptable when vector output is impractical.
- Prefer vector output; raster images should normally be at least 300 DPI.
- Ensure fonts remain at least 10 pt after scaling, axes are labeled, and lines are
  distinguishable and identified.
- Use a restrained, accessible palette rather than relying on color alone.
- Make every figure understandable from its caption and labels.

Original quantity targets: a 50+ page survey has at least 10 tables and 6 figures;
a 30-page survey has at least 5 tables and 3 figures. Add visuals only when they
carry a real comparison, explanation, or finding.

## 5. Peer Review Simulation

Input: compiled manuscript. Output: scores and prioritized weaknesses routed back
to modules 1–4.

### Reviewer lenses

| Persona | Focus | Source weighting cue |
| --- | --- | ---: |
| Experimentalist | statistical rigor, baselines, replication | Experimental 30% |
| Theorist | definitions, proofs, taxonomy | Technical depth 35% |
| Perfectionist | writing, figures, formatting | Clarity 30% |
| Synthesizer | cross-cutting analysis and gaps | Novelty 25% |
| Newcomer | accessibility, definitions, examples | Clarity 35% |

Use three to five lenses per round. Score them independently before synthesis to
reduce anchoring. The source dimensions are novelty, comprehensiveness, clarity,
technical depth, and experimental validation; the final score is the median.

Source calibration: 6.0=workshop, 7.0=main conference, 8.0=strong accept/top 20%,
9.0=oral. These labels are internal heuristics, not predictions of real review.

Anti-inflation rules:

- Cap the first round at 7.0.
- Increase by no more than 1.5 points per round.
- Preserve at least one unresolved weakness unless the evidence genuinely supports
  none.
- Seek viewpoint diversity. A different model is optional and requires available,
  authorized access.

Report the overall and per-dimension scores, 3–5 strengths, 3–5 prioritized major
or minor weaknesses, concrete fixes, a recommendation, and a regression check.

## Phase Routing

### Phase 0: topic selection

Answer three questions: scope, angle, and audience.

### Phase 1: draft (source iterations 1–6, target 6.0)

1. Build the skeleton, draft introduction/background, and compile.
2. Retrieve literature and apply initial scoring.
3. Draft core sections and create at least two useful figures where warranted.
4. Classify and verify citations while drafting later sections.
5. Verify citations, compile, and conduct the first review.
6. Route weaknesses, revise, and compile again.

### Phase 2: deep improvement (source iterations 7–9, target 7.5–8.0)

1. Design and execute a justified experiment.
2. Present results and integrate them into the argument.
3. Compile, review, and route fixes.

### Phase 3: sprint (source iteration 10+, target 8.5)

Repeat review -> weakness routing -> fix -> compile -> review. Stop when the agreed
quality target is met, the score changes by <=0.3 for two rounds, iteration exceeds
12, or the user's time/resource limit is reached.

## Weakness Routing

| Weakness | Route | Action |
| --- | --- | --- |
| Citation coverage insufficient | Literature | targeted retrieval and scoring |
| Too many arXiv-only references | Literature | verify accepted versions |
| Missing recent papers | Literature | search the current research window |
| Structure unclear | Structure | reorganize and add transitions |
| Analysis lacks depth | Structure | add critical assessment |
| Taxonomy not novel | Structure | reconsider axes and differentiator |
| Claims too strong | Structure | weaken wording or strengthen evidence |
| No experiments | Experiment | decide whether a pilot addresses a claim |
| Experiment not rigorous | Experiment | improve controls, trials, or ablation |
| Tables incomparable | Figures/tables | regroup and add a meaningful delta column |
| Missing visualization | Figures/tables | add a justified figure |
| No error bars | Figures/tables | show appropriate uncertainty |

## Quality Gates

### Gate 1: literature

- Citations >=80 for a draft or >=3 per page for a final manuscript.
- Work within one year >=40%; accepted work >=30%; arXiv-only <=60%.
- Verification rate >=80%; every taxonomy cell has at least two A/B references.

### Gate 2: experiment

- Clear preregistered hypothesis and planned statistical test or confidence interval.
- At least three trials with variability reported when repeated trials apply.
- No unaddressed ceiling or floor effect.
- Explicit connection to a paper claim.

### Gate 3: structure

- Compiles with no errors or undefined references.
- Source guide target: each `.tex` file <=300 lines.
- Abstract and conclusion align; sections have transitions; core sections include
  critical assessment; terminology is consistent.
- Include a formal claim only when useful and appropriately qualified.

### Gate 4: figures and tables

- Source target for a full survey: at least 10 tables and 6 figures.
- No vertical table rules; every visual carries a non-trivial insight and is cited
  in the text.
- Captions state conclusions; experimental data includes suitable uncertainty.

### Gate 5: final review

- Applicable gates 1–4 pass.
- The manuscript compiles cleanly.
- The internal review reaches the agreed target.
- Previously fixed weaknesses have not regressed.
- Version and snapshot are saved using the project's existing versioning practice.

Source: [Deli AutoResearch — Scientific Paper Writing Skill Group v2.0](https://victorchen96.github.io/auto_research/skill/paper-writing.html), June 2026.
