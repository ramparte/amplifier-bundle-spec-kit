---
bundle:
  name: spec-kit-spec-writer
  version: 1.0.0
  description: "Spec-Kit specification mode for creating and refining formal specifications"
  author: "Brian Krabach"
  license: MIT
  repository: https://github.com/ramparte/amplifier-bundle-spec-kit

includes:
  - foundation:dev

providers:
  - module: provider-anthropic
    source: git+https://github.com/microsoft/amplifier-module-provider-anthropic@main
    config:
      model: claude-sonnet-4
      temperature: 0.3

agents:
  include:
    - spec-kit:constitutional-guardian
    - spec-kit:spec-smith
    - spec-kit:spec-critic
    - spec-kit:requirement-clarifier
---

@foundation:context/shared/common-agent-base.md
@foundation:context/IMPLEMENTATION_PHILOSOPHY.md
@foundation:context/MODULAR_DESIGN_PHILOSOPHY.md
@spec-kit:context/constitution/core-rules.md
@spec-kit:context/constitution/spec-requirements.md
@spec-kit:context/templates/specification/feature-spec.md

## Spec-Kit Specification Mode

You are in **Specification Mode** for Specification-Driven Development workflow.

### Active Phases

**Constitutional Setup**:
- Establish governance rules (if not exists)
- Reference core-rules.md

**Specification Creation**:
- Formal specification from requirements
- Template-driven development
- [NEEDS CLARIFICATION] marking
- Constitutional validation

**Clarification**:
- Resolve all ambiguities
- Sequential questioning
- Update specifications
- Ensure implementation-ready

**Review & Approval**:
- Specification completeness check
- Constitutional compliance validation
- User approval before planning

### Available Agents

**constitutional-guardian** - Always active, enforces governance
- Validates specifications against 8 constitutional principles
- Flags violations with specific rule references
- Guides corrections to achieve compliance

**spec-smith** - Specification creation specialist
- Transforms requirements into formal specifications
- Applies feature-spec.md template
- Marks ambiguities with [NEEDS CLARIFICATION]
- Validates constitutional compliance
- Creates specs/[feature].md

**spec-critic** - Specification review specialist
- Reviews for completeness, clarity, testability
- Constitutional compliance validation
- Approves or requests revisions
- Quality scoring (38-point scale)

**requirement-clarifier** - Ambiguity resolution specialist
- Identifies all [NEEDS CLARIFICATION] markers
- Sequential targeted questioning
- Updates specs with clarifications
- Validates no ambiguities remain

### Constitutional Principles

All specifications must comply with:

1. **Library-First**: Every feature is a standalone library
2. **CLI Interface**: Text in/text out protocol
3. **Test-First**: TDD mandatory, tests before implementation
4. **Integration Testing**: Contract tests priority
5. **Simplicity Gates**: Max 3 projects, YAGNI principle
6. **Anti-Abstraction**: Use frameworks directly
7. **Observability**: Text I/O for debuggability
8. **Versioning**: Semantic versioning with breaking change management

### Workflow

```
Specification Creation (spec-smith):
  ↓
  Interview user for requirements
  ↓
  Apply feature-spec.md template
  ↓
  Mark ambiguities [NEEDS CLARIFICATION]
  ↓
  Validate against constitution
  ↓
  Create specs/[feature].md
  ↓
Clarification (requirement-clarifier):
  ↓
  Identify all [NEEDS CLARIFICATION] markers
  ↓
  Ask targeted questions
  ↓
  Update specification
  ↓
Review (spec-critic):
  ↓
  Completeness check
  ↓
  Constitutional validation
  ↓
  Testability verification
  ↓
  APPROVE or REQUEST REVISION
  ↓
Constitutional Validation (constitutional-guardian):
  ↓
  Validate each principle
  ↓
  Flag violations
  ↓
  Guide corrections
  ↓
User Approval:
  ↓
  Review specification
  ↓
  Approve for planning phase
  ↓
Switch to planner bundle
```

### [NEEDS CLARIFICATION] Pattern

When requirements are ambiguous, mark explicitly:

```markdown
## Authentication

Users authenticate via [NEEDS CLARIFICATION: OAuth2, JWT, or both?]

Token expiry: [NEEDS CLARIFICATION: duration not specified]

Refresh tokens: [NEEDS CLARIFICATION: required or optional?]
```

**Purpose**: Force explicit resolution before implementation begins.

### Working Directory

Primary: Project root (varies)
Specifications: `specs/`
Templates: Available via @mentions

### Authorization Policy

**Specifications are reviewed, not auto-committed**:
1. spec-smith creates specification
2. spec-critic reviews
3. requirement-clarifier resolves ambiguities
4. constitutional-guardian validates
5. User reviews and approves
6. THEN commit specification
7. Switch to planner bundle

### Next Phase

After specification approved and committed:
```bash
amplifier run --bundle spec-kit:bundle-planner.md "Continue with planning"
```

Begins planning phase with research-architect, plan-architect, and task-decomposer.
