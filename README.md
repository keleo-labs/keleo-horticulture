# keleo-template

A template repository for creating and organizing practices and methods using the [Keleo Studio](https://github.com/keleo-labs/keleo-studio) application.

## Overview

This template provides a standardized directory structure for collecting JSON-formatted practices that keleo-studio language schema. The practices created here can be authored, visualized, and managed using the Keleo Studio web application.

## What is Keleo Studio?

Keleo Studio (also known as Adoption Framework) is a comprehensive practice management and method composition system that enables teams to:

- **Author Practices**: Create software engineering practices with schema validation
- **Compose Methods**: Build methods from baseline practices and extensions
- **Visualize Workflows**: Generate Kanban pattern boards and flow diagrams
- **Manage Libraries**: Browse, import, export, and organize practice collections

## Directory Structure

```
keleo-template/
├── baseline/          # PracticeBaseline JSON files (kernel practices)
├── methods/           # Method JSON files (composed practices)
└── practices/         # Practice JSON files (extensions)
```

### Directory Purposes

- **baseline/**: Contains foundational kernel practices that define core elements (Alphas, States, Activities, WorkProducts, Competencies, etc.)
- **practices/**: Contains practice extensions that build upon baselines with specific methodologies
- **methods/**: Contains composed methods that combine a baseline with multiple practices

## Getting Started

### Prerequisites

- Access to Keleo Studio - see the [main repository](https://github.com/keleo-labs/keleo-studio)
- Basic understanding of SEMAT language concepts
- A source methodology or documentation you want to convert into practices

### Workflow

1. **Set up Keleo Studio**: Clone and run the Adoption Framework application (typically at `../adoptionframework`)
2. **Generate Practices**: Use the LLM-based generation process with the prompts in the Keleo Studio `prompts and instructions/` folder
3. **Organize Output**: Place generated JSON files in the appropriate directories:
   - New kernel practices → `baseline/`
   - Practice extensions → `practices/`
   - Composed methods → `methods/`
4. **Validate**: Use Keleo Studio's validation tools to ensure schema compliance
5. **Visualize**: Import into Keleo Studio to view Kanban boards and flow diagrams

## Generating Practices with LLMs

Keleo Studio includes comprehensive prompts for generating practices from source documentation. The main approaches are:

### Full Process (11 Phases)

Use `full-process-gem.md` for complete practice generation with rigorous validation:

1. Load the baseline kernel and schema
2. Provide source documentation (methodology, framework, or workflow)
3. Work through 11 phases: Personas → Alphas → WorkProducts → Activities → PersonaGroups → Narratives → Lifecycle Patterns → Narrative Patterns → Practice Formation → Logical Integrity → Final Output
4. Output validated JSON practices/methods

### Two-Phase Research Process

Use `phase 1 gem.md` and `phase 2 gem.md` for a research-first approach:

- **Phase 1**: Generate human-readable research report analyzing the source methodology
- **Phase 2**: Convert the research report into validated JSON

## Practice Components

Practices in this system contain:

- **Alphas**: Essential elements of concern (e.g., Platform, Team, Opportunity)
- **States**: Progression checkpoints for alphas
- **Activities**: Work that contributes to alpha states
- **WorkProducts**: Artifacts produced by activities
- **Patterns**: Temporal progressions showing how practices unfold
- **Personas & PersonaGroups**: Roles and teams involved
- **Competencies**: Required skills mapped to personas
- **Narratives**: Contextual storytelling for elements

## Validation

All practices must conform to the JSON schema defined in Keleo Studio:

```bash
# Validate a practice file using Keleo Studio
cd ../adoptionframework
node validate-schema.js path/to/practice.json
```

## Integration with Keleo Studio

To use these practices in Keleo Studio:

1. Start the Keleo Studio development server
2. Use the **Library** feature to import practice JSON files
3. Use the **Practice Author** to edit and refine practices
4. Use the **Method Builder** to compose methods from practices
5. Use the **Flow Visualizer** to view Kanban pattern boards

## Example Practice Libraries

See the Keleo Studio repository for reference examples:
- `practices/adoption-library.json` - Main practice library
- `practices/team-topologies-method.json` - Example composed method

## License

This template repository is licensed under the Apache License 2.0.

## Additional Resources

- [Keleo Studio Documentation](https://github.com/keleo-labs/keleo-studio) (Private repository)
- [SEMAT Essence Framework](https://www.semat.org/)
- Keleo Studio `prompts and instructions/` folder for LLM generation guides
