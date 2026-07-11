# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a template repository for collecting and organizing JSON-formatted software engineering practices and methods. It is designed to work with **Keleo Studio** , a Next.js application for authoring, composing, and visualizing practices derived and adapted from the SEMAT practice language.

## Relationship with Keleo Studio

This template repository stores practice JSON files that can be:
- Authored and edited using Keleo Studio's Practice Author interface
- Validated against the JSON schema defined in `language.schema.json`
- Composed into methods using Keleo Studio's Method Builder
- Visualized as Kanban pattern boards and Sankey flow diagrams

**Keleo Studio location**: Typically at `../adoptionframework` relative to this repository

## Directory Structure

```
keleo-template/
├── baseline/          # PracticeBaseline JSON files
├── methods/           # Method JSON files (composed practices)
└── practices/         # Practice JSON files (extensions)
```

### File Types

- **PracticeBaseline** (`baseline/`): Kernel practices defining core Alphas, ActivitySpaces, Competencies, and NarrativeTypes
- **Practice** (`practices/`): Extensions that build on a baseline using `baselinePracticeName` reference
- **Method** (`methods/`): Compositions of multiple practices, can use either:
  - Full embedded objects (`baselinePractice` + `practices` array)
  - String references (`baselinePracticeName` + `practiceNames` array)

## Core Concepts

### Practice Language Elements

Based on SEMAT language:

- **Alphas**: Essential elements of concern (e.g., Platform, Team, Opportunity, Stakeholders)
- **States**: Progressive maturity checkpoints for Alphas (typically 3-6 states)
- **Activities**: Work that contributes to advancing Alpha states
- **ActivitySpaces**: Categories organizing types of work by focus area
- **WorkProducts**: Artifacts produced by activities with Levels of Detail (LODs)
- **Competencies**: Skills required for personas, with proficiency levels

New concepts:

- **Personas & PersonaGroups**: Roles and teams mapped to activities
- **Patterns**: Temporal workflows with PatternViews (lifecycle or narrative-based)
- **Narratives**: Storytelling contexts using NarrativeTypes (STAR, StoryBrand, ABT, Epic, Lifecycle, etc.)

### Focus Areas

The Platform Adoption Essentials baseline organizes content into three Areas of Concern:

- **Value**: Business justification, financial management, stakeholder alignment
- **Solution**: Architecture, implementation, platform design, hosted items
- **Endeavor**: Team execution, processes, policies, organizational change

## Working with Practice Files

### Validation

Before editing or after creating practice JSON files, validate them:

```bash
cd ../keleo-studio
node validate-schema.js path/to/practice.json
```

Full validation (includes logical integrity checks):

```bash
cd ../keleo-studio
node validate-full.js path/to/practice.json
```

### Key Schema Constraints

When creating or editing practices:

1. **String References Only**: Use exact string names when referencing elements (never embed full objects when string is required)
2. **Baseline Declaration**: Practice files must include `"baselinePracticeName": "Platform Adoption Essentials"`
3. **Alpha Contributions**: New Alphas must declare `contributesTo` referencing a baseline or practice dependency Alpha
4. **Activity Spaces**: Activities must map to valid `activitySpaceName` from baseline
5. **Competency Mapping**: Personas must have non-empty `competencies` arrays with exact matches to baseline Competency names
6. **PersonaGroup Hierarchy**: Personas belong to PersonaGroups; Activities reference PersonaGroups (not Personas directly) in `involves` array
7. **Narrative Structure**: Every Narrative object requires both `name` AND `narrativeName` properties
8. **Work Product LODs**: WorkProducts must have minimum 3 Levels of Detail
9. **Alpha States**: When redeclaring baseline Alphas, preserve state names and count (can enrich with checklists)

### Practice Element Aliases

Use `practiceElementAliases` array to map vendor-specific or localized terminology to canonical baseline names. The alias is for human readability only - all structural references must use the original baseline name.

## Generating Practices with LLMs

Keleo Studio includes comprehensive LLM prompts in `../adoptionframework/prompts and instructions/`:

### Full Process (full-process-gem.md)

11-phase analytical pipeline for generating validated practices:
1. Initial Personas
2. Alphas (with baseline mutation vs. extension logic)
3. WorkProducts (with LODs mapped to maturity rubric)
4. Activities (mapped to ActivitySpaces)
5. Personas and PersonaGroups Links
6. Narratives (contextual storytelling)
7. Lifecycle Patterns (phase-gated execution)
8. Narrative Patterns (STAR, StoryBrand, ABT, etc.)
9. Practice Formation (single practice or method composition)
10. Logical Integrity (referential integrity, tagging, metadata)
11. Drafting Operational Elements (final schema validation)

### Two-Phase Research Process

- **phase 1 gem.md**: Generate human-readable research report analyzing source methodology
- **phase 2 gem.md**: Convert research report to validated JSON

### Critical Anti-Hallucination Directives

When using LLM prompts:
- Treat baseline as custom, proprietary ontology (not standard OMG Essence)
- Actively suppress pre-trained knowledge of standard Essence elements
- Only use elements explicitly present in uploaded baseline JSON
- Validate all string references against extracted baseline lists
- Zero-Truncation Policy: never use placeholders or omit array content

## Common Development Tasks

### Creating a New Practice

1. Identify source methodology/documentation
2. Determine if it extends existing baseline or requires new baseline
3. Use Keleo Studio LLM prompts to generate practice JSON
4. Validate with `validate-schema.js`
5. Place in `practices/` directory
6. Import into Keleo Studio for visualization and refinement

### Creating a Method

1. Identify constituent practices (must already exist or be generated)
2. Determine practice dependencies using `practiceDependencyNames`
3. Compose method with baseline + practices
4. Create lifecycle pattern to orchestrate practices if needed
5. Validate with `validate-full.js`
6. Place in `methods/` directory

### Validating Practice Integrity

Check for common issues:
- Empty or missing arrays (Personas, Activities, States)
- Orphaned elements (PersonaGroups not referenced in Activities)
- Invalid string references (contributesTo, activitySpaceName not matching baseline)
- Missing narrative contexts in Patterns
- Incomplete Levels of Detail in WorkProducts
- Empty competencies arrays in Personas

## Integration with Keleo Studio

### Running Keleo Studio

```bash
cd ../keleo-studio
npm install
npm run dev
```

Access at http://localhost:3000

### Key Pages

- `/` - Dashboard (access all features)
- `/practice-author` - Create/edit practices with WYSIWYG editor
- `/method-builder` - Compose methods via drag-and-drop
- `/library` - Browse and manage practice library
- `/flow-visualizer` - View Kanban pattern boards

### API Endpoints

```
GET    /api/documents              # List all documents
GET    /api/documents/:id          # Get document by ID
POST   /api/documents              # Create document
PUT    /api/documents/:id          # Update document
DELETE /api/documents/:id          # Delete document
POST   /api/documents/resolve-for-render  # Resolve practice with dependencies
POST   /api/pdf                    # Generate PDF from practice/method
```

## Storage

Practices can be stored as:
- **File Storage** (default): JSON files in filesystem
- **MongoDB Storage**: Documents in MongoDB collections

Set via `STORAGE_TYPE` environment variable in Keleo Studio.

## License

This repository is licensed under Apache License 2.0.
