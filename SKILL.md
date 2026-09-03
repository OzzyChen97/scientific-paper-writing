---
name: scientific-paper-writing
description: >-
  Orchestrate end-to-end scientific survey-paper production across literature
  retrieval, manuscript structure, experiment design, figures and tables, and
  iterative peer-review simulation. Use for long-form survey planning, drafting,
  evidence-backed revision, or quality-gated paper sprints; use a narrower writing
  skill for ordinary paragraph-level editing.
metadata:
  short-description: Build and iteratively improve scientific survey papers
  source: https://victorchen96.github.io/auto_research/skill/paper-writing.html
---

# Scientific Paper Writing

Treat paper production as five coordinated modules: literature survey, structure
and logic, experiment design, figures and tables, and peer-review simulation.
Use only the modules needed for the user's request; do not force the full pipeline
onto a focused writing or review task.

For the detailed thresholds, routing table, artifact contracts, and review rubric,
read [references/protocol.md](references/protocol.md). Read the whole reference
when running the complete paper workflow. For a narrow task, read only its named
module and any applicable quality gate.

## Operating rules

- Start a new paper by establishing its scope, differentiating angle, and intended
  audience. If repository files already answer these questions, use that evidence.
- Maintain traceability from claims to verified sources or experimental results.
  Never invent citations, venues, acceptance status, measurements, or review
  outcomes.
- Treat the protocol's counts and scores as configurable process heuristics, not
  proof of scholarly quality or likely venue acceptance. Adapt them to the user's
  venue, genre, length, deadline, and available evidence.
- Use literature-quality scores for triage, then apply scholarly judgment. Do not
  exclude relevant work solely because of author affiliation, institution, venue,
  citation count, or recency.
- Decide the statistical analysis before inspecting outcomes when designing new
  experiments. Report null and negative findings, uncertainty, limitations, and
  deviations from the plan.
- Obtain user authorization before paid API calls, cluster/GPU jobs, submissions,
  or other consequential external actions. A paper-writing request alone does not
  authorize those actions.
- Simulate reviewer personas within the current task unless the user explicitly
  asks for delegated or parallel review.
- Preserve existing manuscript conventions and user-authored work. Keep generated
  artifacts in the project layout the user selected.

## Workflow

1. **Topic selection:** establish scope, angle, and audience.
2. **Draft:** create a coherent skeleton, survey and verify the literature, draft
   core sections, add early figures, compile, review, and route fixes.
3. **Deep improvement:** design only experiments that support or challenge a
   specific claim; present results and integrate them into the argument.
4. **Sprint:** alternate review, weakness routing, revision, compilation, and
   regression checks until the agreed stopping condition is met.

Do not report a gate as passed without checking its observable criteria. When a
criterion cannot be checked, label it unverified and explain what evidence is
missing.

## Default deliverables

- Literature: `references.bib` and `citation_plan.jsonl`
- Manuscript: modular `sections/*.tex` or the project's existing source format
- Experiments: `results.json` and `experiment_summary.md`
- Presentation: `figures/*` and `tables/*`
- Review: per-dimension scores, prioritized weaknesses, actionable fixes,
  recommendation, and regression check

Source adaptation: Deli AutoResearch, “Scientific Paper Writing Skill Group
v2.0,” June 2026. The source repository publishes an HTML guide rather than an
installable `SKILL.md`; this package adds Codex-compatible frontmatter and
authorization boundaries while retaining its operational protocol.
