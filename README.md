# Scientific Paper Writing

[![License](https://img.shields.io/badge/license-Apache--2.0-blue.svg)](LICENSE)

A Codex skill for planning, drafting, evaluating, and iteratively improving
scientific survey papers. It coordinates five modules:

- literature survey and citation verification;
- manuscript structure and argumentation;
- experiment design and reporting;
- academic figures and tables;
- multi-perspective peer-review simulation.

The workflow emphasizes claim-to-evidence traceability, explicit quality gates,
honest uncertainty, and configurable process heuristics rather than promises of
venue acceptance.

## Install

Clone the repository into your Codex skills directory:

```bash
git clone https://github.com/OzzyChen97/scientific-paper-writing.git \
  ~/.codex/skills/scientific-paper-writing
```

Then invoke it in Codex with a prompt such as:

```text
$scientific-paper-writing Design a literature-grounded plan for a survey on
embodied vision-language-action models, including scope, taxonomy, evidence
strategy, and review gates.
```

## Repository layout

```text
.
├── SKILL.md                 # Skill entrypoint and operating rules
├── agents/openai.yaml       # Codex UI metadata
└── references/protocol.md   # Detailed modules, routing, and quality gates
```

## Design principles

- Verify citations and experimental claims; never fabricate scholarly evidence.
- Treat numeric targets and review scores as adaptable heuristics.
- Plan statistical analysis before inspecting experimental outcomes.
- Report null results, uncertainty, limitations, and deviations.
- Require explicit authorization for paid APIs, compute jobs, and submissions.

## Attribution

This package adapts Deli AutoResearch's *Scientific Paper Writing Skill Group
v2.0* into a Codex-compatible skill with YAML frontmatter, progressive disclosure,
and explicit authorization boundaries. See [NOTICE](NOTICE) for lineage and
modification details.

## License

Licensed under the [Apache License 2.0](LICENSE).

