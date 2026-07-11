# Keleo Horticulture

A demonstration of [keleo-language](https://github.com/keleo-labs/keleo-language) being used to describe methods and practices outside of software engineering. This project models professional horticulture — covering biological systems, production operations, and professional practice — as structured, composable practices.

## Published Method

A method composed from this baseline and practices is published at:

- **Documentation site**: https://keleo-labs.github.io/keleo-horticulture-docs/
- **Source repository**: https://github.com/keleo-labs/keleo-horticulture-docs

## What's in This Repository

### Baseline: Horticulture Essentials

The foundational baseline (`baseline/horticulture-essentials.json`) defines the essential elements for professional horticulture, organized across three areas of concern:

- **Biological Systems** — living plants, their growing environments, and ecological interactions
- **Production Operations** — infrastructure, cultivation methods, technology, and resource management
- **Professional Practice** — competencies, business operations, regulatory compliance, and governance

It includes 11 Alphas tracking maturity across the domain:

| Area | Alphas |
|------|--------|
| Biological Systems | Plant Health & Development, Growing Environment, Plant Protection, Biosecurity & Ecosystem Health, Sustainability & Environmental Stewardship |
| Production Operations | Production System Architecture, Technical Infrastructure, Resource Management, Digital Integration |
| Professional Practice | Business Operations & Governance, Regulatory Compliance & Standards |

8 Competencies define the skills required by horticultural practitioners, from Plant Science Knowledge and Growing Media Management through to Business & Project Management and Professional Practice.

9 Activity Spaces organize work into categories such as Cultivate & Maintain Plant Health, Protect Plants & Ecosystems, Deploy & Maintain Technical Infrastructure, and Ensure Compliance & Quality.

### Practice: Horticulture Foundations

The practice extension (`practices/horticulture-foundations.json`) builds on the baseline with three embedded sub-practices:

- **Plant Biology & Protection** — evidence-based cultivation, integrated protection, and ecological management
- **Production Technology & Operations** — design, construction, and optimization of production infrastructure and digital systems
- **Professional Practice & Governance** — business management, regulatory compliance, workforce development, and professional standards

## Directory Structure

```
keleo-horticulture/
├── baseline/          # Foundational kernel practice (Horticulture Essentials)
├── methods/           # Composed methods combining baseline + practices
└── practices/         # Practice extensions (Horticulture Foundations)
```

## About Keleo Language

[Keleo Language](https://github.com/keleo-labs/keleo-language) is a JSON-based practice language derived from SEMAT Essence. While SEMAT was originally designed for software engineering, keleo-language generalizes the core concepts — Alphas, States, Activities, Competencies, Patterns, and Narratives — so they can describe methods and practices in any domain.

This repository demonstrates that generality by applying the language to horticulture.

## Tooling

- **[Keleo Studio](https://github.com/keleo-labs/keleo-studio)** — a Next.js application for authoring, composing, and visualizing practices. Use it to edit practice JSON, compose methods, and generate Kanban pattern boards and flow diagrams.
- **[keleo-pgem-llm](https://github.com/keleo-labs/keleo-pgem-llm)** — skills for Claude that assist with initial practice creation from source documentation. Useful for bootstrapping a new practice from an existing methodology or framework.

## License

Apache License 2.0
