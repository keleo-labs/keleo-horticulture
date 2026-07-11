# Methods

This directory contains **Method** JSON files - composed practices that combine a baseline with multiple practice extensions to create a complete, cohesive methodology.

## What is a Method?

A Method is a complete approach to software engineering work, composed of:
- **One baseline practice** (the foundation)
- **Multiple practice extensions** (specific guidance areas)
- **Optional method-level narratives** (overarching story)

Methods represent full methodologies like "Azure Well-Architected Method", "Team Topologies Method", or "Platform Engineering Practice".

## Method vs Practice

| Aspect | Practice | Method |
|--------|----------|--------|
| **Scope** | Single area of concern | Complete methodology |
| **Structure** | Extends baseline | Composes multiple practices |
| **Reference** | `baselinePracticeName` | `baselinePracticeName` + `practiceNames` |
| **Standalone** | Focused guidance | Complete approach |
| **Visualization** | Single practice view | Merged composite view |

## Structure

A Method can be represented in two formats:

### Format 1: String References (Compact)

Recommended for version control and interchange:

```json
{
  "name": "Method Name",
  "description": "What this method provides",
  "baselinePracticeName": "Platform Adoption Essentials",
  "practiceNames": [
    "Practice One",
    "Practice Two",
    "Practice Three"
  ],
  "narratives": [...],
  "tags": {...},
  "authors": [...],
  "createdAt": "ISO 8601 date",
  "updatedAt": "ISO 8601 date",
  "version": "1.0.0",
  "keywords": [...]
}
```

### Format 2: Full Embedded Objects

Recommended for complete export and standalone distribution:

```json
{
  "name": "Method Name",
  "description": "What this method provides",
  "baselinePractice": {
    "name": "Platform Adoption Essentials",
    "focuses": [...],
    "alphas": [...],
    "activitySpaces": [...],
    "competencies": [...]
  },
  "practices": [
    {
      "name": "Practice One",
      "alphas": [...],
      "activities": [...]
    },
    {
      "name": "Practice Two",
      "alphas": [...],
      "activities": [...]
    }
  ],
  "narratives": [...],
  "tags": {...},
  "authors": [...],
  "createdAt": "ISO 8601 date",
  "updatedAt": "ISO 8601 date",
  "version": "1.0.0"
}
```

**Important**: Use EITHER `baselinePractice` OR `baselinePracticeName` (NOT BOTH). The presence of `practices`, `practiceNames`, or `baselinePractice` discriminates a Method from a Practice.

## Method Composition

### Composition Order

Practices are merged in order:
1. **Baseline** provides foundation (Focuses, core Alphas, ActivitySpaces, Competencies)
2. **Practice dependencies** resolve recursively
3. **Practices** merge in array order

### Merge Algorithm

The merge algorithm:
- **Preserves hierarchy**: Baseline descriptions override extensions
- **Unions arrays**: Combines named elements by key
- **Merges tags**: Combines structured tags by bucket
- **Resolves focus**: Prefers explicit focus over implicit placeholders
- **Aggregates alphas**: Auto-populates `supportingAlphas` from `contributesTo`

Elements with the same `name` are merged; unique elements are added.

### Dependency Resolution

If practices declare `practiceDependencyNames`, the resolver:
- Recursively loads dependencies
- Detects circular references
- Merges dependencies before dependent practices
- Caches resolved practices

## Method-Level Narratives

Methods can include overarching narratives that explain:
- Why the method exists
- What problem it solves
- How it should be applied
- What outcomes to expect

These use the same Narrative structure as practices:

```json
{
  "narratives": [
    {
      "name": "method-overview",
      "narrativeName": "Method Overview",
      "description": "High-level method purpose",
      "narrativeTypeName": "Epic",
      "narrativeContexts": [
        {
          "seq": 1,
          "narrativeElementName": "Vision",
          "context": "Our vision is to..."
        }
      ]
    }
  ]
}
```

## When to Create a Method

Create a Method when:
- Combining 2+ practices into a cohesive approach
- Distributing a complete methodology as a single artifact
- Creating a lifecycle practice that orchestrates multiple domain practices
- Packaging a framework (e.g., Azure Well-Architected, DORA metrics)

**Note**: Single practices should be stored in `../practices/` directory, not here.

## Validation

Validate method files using Keleo Studio:

```bash
# Schema validation
cd ../adoptionframework
node validate-schema.js ../keleo-template/methods/your-method.json

# Full validation with composition resolution
node validate-full.js ../keleo-template/methods/your-method.json
```

## Rendering Methods

Keleo Studio can resolve and render methods:

```bash
# Programmatically resolve a method
POST /api/documents/resolve-for-render
{
  "documentJson": { /* method JSON */ }
}
```

The resolver:
1. Loads the baseline practice
2. Recursively resolves practice dependencies
3. Merges all practices in order
4. Returns a composite practice with all elements merged

## Common Method Patterns

### Domain + Lifecycle Pattern

Multiple domain practices orchestrated by a lifecycle:

```
azure-waf-method/
  - Baseline: Platform Adoption Essentials
  - Practices:
    - reliability-practice
    - security-practice
    - cost-optimization-practice
    - performance-practice
    - waf-lifecycle (depends on all pillars)
```

The lifecycle practice contains a Pattern that:
- References Alphas from all domain practices
- Shows how they progress together through assessment phases
- Coordinates activities across multiple concerns

### Layered Methodology

Foundational → Advanced practices:

```
platform-engineering-method/
  - Baseline: Platform Adoption Essentials
  - Practices:
    - platform-foundation (core platform concepts)
    - developer-experience (extends foundation)
    - observability-practice (extends foundation)
    - golden-path-practice (depends on all)
```

### Framework Translation

Translating existing frameworks:

```
team-topologies-method/
  - Baseline: Platform Adoption Essentials
  - Practices:
    - team-types-practice
    - interaction-modes-practice
    - cognitive-load-practice
    - team-topologies-lifecycle
```

## Visualizing Methods

In Keleo Studio:

1. **Library View**: Browse methods and their constituent practices
2. **Method Builder**: Drag-and-drop composition interface
3. **Flow Visualizer**: View merged Kanban pattern boards
4. **PDF Export**: Generate human-readable reports

The visualizations show the merged, composite view of all practices.

## Exporting Methods

Methods can be exported:

### As String References
- Small file size
- Requires practice library to resolve
- Version control friendly
- Good for collaborative development

### As Full Embedded Objects
- Large file size
- Self-contained and portable
- No dependencies needed
- Good for distribution and archival

Choose format based on use case.

## Tags for Organization

Use structured tags to classify methods:

```json
{
  "tags": {
    "domainTags": ["cloud", "platform engineering", "azure"],
    "lifecycleTags": ["complete methodology"],
    "organizationalTags": ["enterprise", "multi-team", "scaled"]
  }
}
```

## Example Methods

See the Keleo Studio repository for reference:
- `team-topologies-method.json` - Complete Team Topologies methodology

## Creating a New Method

### Approach 1: Compose Existing Practices

1. Identify existing practices to combine
2. Create method JSON with `practiceNames` array
3. Optionally add method-level narratives
4. Validate composition resolves correctly

### Approach 2: Generate Complete Method

1. Identify comprehensive source material
2. Use LLM generation with multi-practice output:
   - `../adoptionframework/prompts and instructions/full-process-gem.md`
   - Phase 9 handles multi-practice → Method wrapping
3. Validate complete method structure
4. Import into Keleo Studio

### Approach 3: Method Builder UI

1. Open Keleo Studio Method Builder
2. Select baseline practice
3. Drag practices from library
4. Arrange in dependency order
5. Add method narratives
6. Export to JSON

## Practice Dependency Graph

Methods implicitly create dependency graphs:

```
Method: Azure WAF
  ├─ Baseline: Platform Adoption Essentials
  ├─ Practice: Reliability
  ├─ Practice: Security
  ├─ Practice: Cost Optimization
  └─ Practice: WAF Lifecycle
       └─ Dependencies: [Reliability, Security, Cost Optimization]
```

The resolver ensures proper ordering and handles transitive dependencies.

## Versioning Methods

Methods should be versioned to track evolution:

```json
{
  "name": "Platform Engineering Method",
  "version": "2.1.0",
  "updatedAt": "2026-05-15T10:30:00Z"
}
```

When practices change:
- Update method version
- Document changes in description or narratives
- Consider whether to update practice references

## Additional Resources

- See root README.md for overall workflow
- See `../baseline/README.md` for baseline concepts
- See `../practices/README.md` for practice creation
- See `../adoptionframework/docs/SYSTEM_ARCHITECTURE.md` for merge algorithm details
- See `../adoptionframework/web/src/lib/methodMerge/` for implementation
