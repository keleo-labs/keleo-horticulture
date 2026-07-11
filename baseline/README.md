# Baseline Practices

This directory contains **PracticeBaseline** JSON files, also known as "kernel" practices. These are foundational practices that define the core ontology and elements that other practices build upon.

## What is a PracticeBaseline?

A PracticeBaseline serves as the foundation of a practice ecosystem. It defines:

- **Focuses**: The main areas of concern (e.g., Value, Solution, Endeavor)
- **Alphas**: Core conceptual elements with progressive states
- **ActivitySpaces**: Categories organizing types of work
- **Competencies**: Skills and proficiency levels
- **NarrativeTypes**: Story frameworks for contextualizing practices
- **Optionally**: Authors, metadata, keywords, and version information

## Standard Baseline

The primary baseline used in the Keleo ecosystem is:

**Platform Adoption Essentials** (`platform-adoption-kernel.json`)

This baseline defines three Areas of Concern:
- **Value Focus**: Business justification, economics, stakeholders
- **Solution Focus**: Architecture, platform design, implementation
- **Endeavor Focus**: Team execution, processes, organizational change

## Structure

A PracticeBaseline JSON file typically includes:

```json
{
  "name": "Practice Name",
  "description": "What this baseline provides",
  "focuses": [
    {
      "name": "Focus Area",
      "description": "What this focus encompasses"
    }
  ],
  "alphas": [
    {
      "name": "Alpha Name",
      "description": "What this alpha represents",
      "focusName": "Value",
      "states": [...]
    }
  ],
  "activitySpaces": [...],
  "competencies": [...],
  "narrativeTypes": [...],
  "authors": [...],
  "createdAt": "ISO 8601 date",
  "updatedAt": "ISO 8601 date",
  "version": "1.0.0",
  "keywords": [...]
}
```

## Key Elements

### Focuses

Define the organizational structure for Alphas and ActivitySpaces. Typically 2-4 focuses that represent major areas of concern.

### Alphas

Essential elements of concern that have:
- **Name & Description**: What the alpha represents
- **Focus**: Which focus area it belongs to
- **States**: Progressive maturity levels (typically 3-6 states)
- **Checklists**: Criteria for achieving each state

Common baseline Alphas:
- **Opportunity**: Business drivers and value proposition
- **Stakeholders**: People and organizations affected by the initiative
- **Platform**: The technical foundation being built
- **Team**: People doing the work
- **Way Of Working**: Processes and practices being followed

### ActivitySpaces

Categories of work organized by focus area. Activities in practices will reference these spaces. Examples:
- **Exploring**: Discovery and research work
- **Preparing**: Planning and setup activities
- **Operating**: Execution and delivery work
- **Supporting**: Maintenance and support activities

### Competencies

Skills required for performing work, with proficiency levels:
- **Level 1**: Assists (basic awareness)
- **Level 2**: Applies (can perform with guidance)
- **Level 3**: Masters (independent expertise)
- **Level 4**: Adapts (can modify and improve)
- **Level 5**: Innovates (creates new approaches)

### NarrativeTypes

Story frameworks for contextualizing practices and patterns:
- **Lifecycle**: Phase-gated execution models
- **STAR**: Situation, Task, Action, Result
- **StoryBrand**: Three-Act customer journey
- **ABT (And, But, Therefore)**: Micro-narratives
- **Epic**: North star vision
- **User Story**: User-centric intent

## When to Create a New Baseline

Create a new baseline when:
- Starting a completely new domain not covered by existing baselines
- Defining a new organizational ontology
- Establishing a new set of focuses and core concepts

**Note**: Most use cases should extend the existing Platform Adoption Essentials baseline rather than creating a new one.

## Modifying Existing Baselines

Baselines should be relatively stable. If you need to:
- Add domain-specific concepts → Create a Practice extension instead
- Specialize existing Alphas → Create a Practice with new Alphas using `contributesTo`
- Add new work types → Create a Practice with new Activities

## Validation

Validate baseline files using Keleo Studio:

```bash
cd ../adoptionframework
node validate-schema.js ../keleo-template/baseline/your-baseline.json
```

## Usage in Practices

Practices reference baselines using the `baselinePracticeName` property:

```json
{
  "name": "My Practice",
  "baselinePracticeName": "Platform Adoption Essentials",
  "alphas": [...],
  "activities": [...]
}
```

## Immutability Principle

When practices reference a baseline:
- **Identity & Intent Preservation**: Never change Alpha/ActivitySpace names or descriptions
- **Alpha State Integrity**: Cannot add/remove states from baseline Alphas (can only enrich with checklists)
- **Permitted Adaptations**: Can add source-specific checklists, tags, and narratives to states

## Example Baselines

See the Keleo Studio repository for reference:
- `platform-adoption-kernel.json` - The standard Platform Adoption Essentials baseline

## Additional Resources

- See root README.md for overall workflow
- See `../adoptionframework/docs/SCHEMA.md` for complete schema documentation
- See `../adoptionframework/prompts and instructions/` for LLM generation guides
