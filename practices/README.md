# Practices

This directory contains **Practice** JSON files - extensions that build upon a baseline practice to address specific domains, methodologies, or workflows.

## What is a Practice?

A Practice is a discrete, cohesive area of concern that extends a baseline. It represents value-additive guidance for a specific topic within software engineering, such as:

- Platform team formation and operations
- Security practices for cloud platforms
- DevOps automation and CI/CD
- Stakeholder engagement and governance
- Cost optimization and financial management

## Practice vs Baseline

| Aspect | Baseline | Practice |
|--------|----------|----------|
| **Purpose** | Define core ontology | Extend with specific guidance |
| **Elements** | Focuses, core Alphas, ActivitySpaces, Competencies | Specialized Alphas, Activities, WorkProducts |
| **Reference** | None (root) | References baseline via `baselinePracticeName` |
| **Stability** | Stable, rarely changes | Evolves with methodology updates |

## Structure

A Practice JSON file typically includes:

```json
{
  "name": "Practice Name",
  "description": "What this practice provides",
  "baselinePracticeName": "Platform Adoption Essentials",
  "practiceDependencyNames": ["Other Practice"],
  "alphas": [...],
  "activities": [...],
  "workProducts": [...],
  "personas": [...],
  "personaGroups": [...],
  "patterns": [...],
  "narratives": [...],
  "practiceElementAliases": [...],
  "tags": {
    "domainTags": [...],
    "lifecycleTags": [...],
    "organizationalTags": [...]
  },
  "authors": [...],
  "createdAt": "ISO 8601 date",
  "updatedAt": "ISO 8601 date",
  "version": "1.0.0",
  "keywords": [...]
}
```

## Key Elements

### Alphas

Practices can define new Alphas that:
- **Specialize** baseline Alphas using `contributesTo` (e.g., "Platform Team" contributes to baseline "Team")
- **Redeclare** baseline Alphas to enrich with domain-specific checklists
- **Introduce instances** via `alphaInstanceNames` (e.g., "Data Platform", "API Platform")

**Rules**:
- All new Alphas must have `contributesTo` linking to baseline or dependency Alpha
- When redeclaring baseline Alphas, preserve state names and count
- Each Alpha needs 3-6 states with progressive maturity

### Activities

Work that advances Alpha states:
- Must reference a baseline `activitySpaceName`
- Declares `contributesTo` array of AlphaState targets
- Specifies `requiredCompetencies` with proficiency levels
- References `PersonaGroup` names in `involves` array
- Defines `workProducts` contributions

### WorkProducts

Artifacts produced by activities:
- Must have minimum 3 `levelsOfDetail` (LODs)
- LODs map to maturity rubric: Basic → Defined → Applied → Comprehensive
- Each LOD contains checklists for validation
- Can reference `evidencedBy` to link to Alpha state evidence

### Personas & PersonaGroups

- **Personas**: Individual roles with required `competencies` (never empty)
- **PersonaGroups**: Collections of Personas that Activities involve
- **Hierarchy**: Personas → PersonaGroups → Activities (via `involves`)

### Patterns

Temporal workflows showing practice execution:

**Lifecycle Patterns**: Phase-gated execution
- Prerequisites PatternView (seq: 0)
- 3+ Phase PatternViews showing Alpha progression
- Each PatternView includes `alphaStates` and `activities`

**Narrative Patterns**: Story-based frameworks
- STAR (Situation, Task, Action, Result)
- StoryBrand (Three-Act Structure)
- ABT (And, But, Therefore)
- Epic (north star vision)

### Narratives

Contextual storytelling for practices, Alphas, and Activities:
- Each narrative references a `narrativeTypeName` from baseline
- Contains `narrativeContexts` array with content for each narrative element
- Provides the "why" and "how" for practice elements

### Practice Element Aliases

Map vendor-specific or localized terminology to canonical baseline names:

```json
{
  "practiceElementAliases": [
    {
      "aliasName": "Azure Well-Architected Review",
      "practiceElementName": "Architecture Assessment",
      "aliasType": "Activity"
    }
  ]
}
```

**Important**: Aliases are for human readability only. All structural references must use the canonical baseline name.

## Practice Scoping

A Practice should be:
- **Discrete**: Address a specific, cohesive area of concern
- **Value-Additive**: Bring unique value, not just decomposed tasks
- **Maturity-Driving**: Independently advance method maturity
- **Non-Circular**: May depend on other practices but no circular references

## Practice Dependencies

Use `practiceDependencyNames` when:
- Reusing Alphas, Activities, or Personas from other practices
- Building hierarchical practice relationships
- Avoiding duplication across related practices

Dependencies are resolved recursively with cycle detection.

## Validation

Validate practice files using Keleo Studio:

```bash
# Schema validation
cd ../adoptionframework
node validate-schema.js ../keleo-template/practices/your-practice.json

# Full validation (includes logical integrity)
node validate-full.js ../keleo-template/practices/your-practice.json
```

## Common Validation Issues

- **Empty competencies**: Personas must have non-empty `competencies` arrays
- **Invalid contributesTo**: Alpha `contributesTo` must match baseline or dependency Alpha names exactly
- **Invalid activitySpaceName**: Must match baseline ActivitySpace names exactly
- **Orphaned PersonaGroups**: Every PersonaGroup must be referenced in at least one Activity's `involves` array
- **Missing narrative fields**: Narratives require both `name` AND `narrativeName`
- **Insufficient LODs**: WorkProducts need minimum 3 levels of detail
- **Empty arrays**: Avoid truncated or placeholder arrays

## Creating a New Practice

1. **Identify source methodology** (documentation, framework, workflow)
2. **Use LLM generation** with Keleo Studio prompts:
   - Full 11-phase process: `../adoptionframework/prompts and instructions/full-process-gem.md`
   - Two-phase research: `phase 1 gem.md` → `phase 2 gem.md`
3. **Validate** against schema
4. **Import** into Keleo Studio for visualization and refinement
5. **Export** final JSON to this directory

## Multi-Practice Design

When source material covers multiple concerns, create separate practices:

**Example**: Azure Well-Architected Framework might yield:
- `reliability-practice.json` (focused on reliability pillar)
- `security-practice.json` (focused on security pillar)
- `cost-optimization-practice.json` (focused on cost management)
- `azure-waf-lifecycle.json` (orchestrates all pillars via lifecycle pattern)

The lifecycle practice would use `practiceDependencyNames` to reference the pillar practices.

## Tags for Organization

Use structured tags to classify practices:

```json
{
  "tags": {
    "domainTags": ["cloud", "platform engineering", "azure"],
    "lifecycleTags": ["design", "implementation", "optimization"],
    "organizationalTags": ["enterprise", "multi-team"]
  }
}
```

## Example Practices

See the Keleo Studio repository for reference:
- `adoption-library.json` - Comprehensive practice library
- `team-topologies-method.json` - Team design practices

## Usage in Methods

Practices are composed into Methods:

```json
{
  "name": "My Method",
  "baselinePracticeName": "Platform Adoption Essentials",
  "practiceNames": ["Practice One", "Practice Two"]
}
```

## Additional Resources

- See root README.md for overall workflow
- See `../baseline/README.md` for baseline concepts
- See `../methods/README.md` for method composition
- See `../adoptionframework/docs/SCHEMA.md` for complete schema documentation
- See `../adoptionframework/prompts and instructions/` for LLM generation guides
