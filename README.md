# Specification-Driven Development Bundle

> Formal specification-driven workflow for greenfield development with constitutional governance

---

## What This Provides

The **Spec-Kit Bundle** brings GitHub's Specification-Driven Development methodology to Amplifier as native agents and workflows:

- **8 specialized workflow agents** - Each expert in an SDD phase
- **3 phase-specific bundles** - Specification, planning, and implementation modes
- **Constitutional governance** - Explicit quality rules and validation
- **Template-driven development** - Constrain LLMs for consistent specifications
- **Rich artifact generation** - Specs, plans, tasks, research, data models, contracts

### The Core Principle

**"Specifications ARE the source. Code is generated from specifications."**

Traditional: Code guided by specs (drift inevitable)
Spec-Kit: **Specs → Validation → Code** (specs drive everything)

---

## Quick Start

### Installation

```bash
# Run directly from GitHub with a specific bundle
amplifier run --bundle git+https://github.com/ramparte/amplifier-bundle-spec-kit@main:bundle-spec-writer.md "Your task"

# Or clone and run locally
git clone https://github.com/ramparte/amplifier-bundle-spec-kit
```

### Usage

```bash
# Specification Phase (Create formal specifications)
amplifier run --bundle spec-kit:bundle-spec-writer.md "Create API specification for user authentication"

# Planning Phase (Generate implementation plans)
amplifier run --bundle spec-kit:bundle-planner.md "Create implementation plan for specs/auth-api.md"

# Implementation Phase (Execute implementation)
amplifier run --bundle spec-kit:bundle-implementer.md "Implement plans/auth-api.md"
```

---

## When to Use Spec-Kit

### ✅ Use Spec-Kit For

- **Greenfield development** - New features from scratch
- **Formal API design** - External client contracts
- **Constitutional governance** - Need explicit quality rules
- **Multi-team standards** - Shared specification format
- **Complex domain models** - Formal data models and contracts
- **Template-driven work** - Consistent specification structure

### ❌ Don't Use Spec-Kit For

- **Existing codebase changes** - Use DDD collection instead
- **Simple bug fixes** - Overkill for small changes
- **Emergency hotfixes** - Too much process
- **Documentation updates** - Use DDD retcon writing instead

---

## Resources

### Bundles

- **bundle-spec-writer.md** - Specification creation with constitutional validation
- **bundle-planner.md** - Implementation planning with research and task breakdown
- **bundle-implementer.md** - Execution and verification

### Agents (8 specialists)

| Agent | Expertise | Phase |
|-------|-----------|-------|
| **constitutional-guardian** | Governance enforcement, validation | All phases |
| **spec-smith** | Specification creation from requirements | Specify |
| **spec-critic** | Specification review and validation | Specify |
| **requirement-clarifier** | Ambiguity resolution, questioning | Clarify |
| **research-architect** | Technology research and recommendations | Plan |
| **plan-architect** | Implementation planning and task breakdown | Plan |
| **task-decomposer** | Task breakdown with dependencies | Plan |
| **implementation-guide** | Implementation guidance and verification | Implement |

### Context

**Constitution** (Governance Rules):
- `core-rules.md` - Fundamental principles (library-first, TDD, simplicity)
- `spec-requirements.md` - What makes a valid specification
- `quality-standards.md` - Quality thresholds and validation
- `anti-patterns.md` - Common specification mistakes to avoid

**Templates** (Specification Templates):
- Specification templates (api-spec, feature-spec, clarification)
- Planning templates (plan, research, data-model, contract)
- Implementation templates (task, quickstart)

**Examples** (Reference Implementations):
- Example specifications (auth-api, payment-flow, user-profile)
- Example plans (implementation plans, research docs)
- Example tasks (task breakdowns with dependencies)

---

## Workflow Overview

```
Constitutional Setup:
  → Establish governance rules
  ↓
Specification (spec-writer profile):
  → spec-smith creates formal specification
  → spec-critic reviews and validates
  → constitutional-guardian enforces rules
  ↓
Clarification (spec-writer profile):
  → requirement-clarifier resolves ambiguities
  → [NEEDS CLARIFICATION] markers addressed
  ↓
Planning (planner profile):
  → research-architect evaluates technology options
  → plan-architect creates detailed implementation plan
  → task-decomposer breaks into executable tasks
  ↓
Implementation (implementer profile):
  → implementation-guide executes tasks
  → Validates against specification
  → Verifies constitutional compliance
```

---

## Key Techniques

### Constitutional Governance

Explicit quality rules enforced throughout:

**Core Rules**:
- **Library-first principle**: Every feature is a library
- **CLI interface requirement**: Text in/text out protocol
- **Test-first development**: TDD mandatory
- **Simplicity gates**: Max 3 projects, no future-proofing
- **Anti-abstraction**: Use frameworks directly

Reference: `context/constitution/core-rules.md`

### Template-Driven Constraints

Templates constrain LLM behavior for consistency:

- Prevent premature implementation details
- Force explicit uncertainty markers
- Enforce structured thinking
- Constitutional compliance gates
- Hierarchical detail management

Reference: `context/templates/`

### [NEEDS CLARIFICATION] Pattern

Mark ambiguities explicitly:

```markdown
## User Authentication

Users authenticate via [NEEDS CLARIFICATION: OAuth2, JWT, or both?]

Token expiry: [NEEDS CLARIFICATION: Duration not specified]
```

Forces clarification before implementation.

---

## Example Workflow

### Creating a Payment API

```bash
# === Phase 1: Specification ===
uvx --from git+https://github.com/microsoft/amplifier@next amplifier profile use spec-kit:spec-writer

uvx --from git+https://github.com/microsoft/amplifier@next amplifier run "Create API specification for payment processing"

# spec-smith guides through:
# - Constitutional validation
# - Template application
# - Formal contract definition
# - Creates specs/payment-api.md

# spec-critic reviews:
# - Completeness check
# - Constitutional compliance
# - Ambiguity detection

# === Phase 2: Planning ===
uvx --from git+https://github.com/microsoft/amplifier@next amplifier profile use spec-kit:planner

uvx --from git+https://github.com/microsoft/amplifier@next amplifier run "Create implementation plan for specs/payment-api.md"

# research-architect:
# - Evaluates payment gateway options
# - Creates research.md

# plan-architect:
# - Generates plans/payment-implementation.md
# - Defines data models
# - Specifies contracts

# task-decomposer:
# - Breaks into tasks.md
# - Identifies dependencies
# - Marks parallelizable tasks [P]

# === Phase 3: Implementation ===
uvx --from git+https://github.com/microsoft/amplifier@next amplifier profile use spec-kit:implementer

uvx --from git+https://github.com/microsoft/amplifier@next amplifier run "Implement tasks from plans/payment-implementation.md"

# implementation-guide:
# - Executes tasks sequentially
# - Validates against spec
# - Constitutional compliance checks
# - Integration testing
```

---

## Migration from Original Spec-Kit

If you're using the original GitHub spec-kit CLI tool:

### Old Workflow
```bash
specify init my-project

/speckit.constitution
/speckit.specify
/speckit.clarify
/speckit.plan
/speckit.tasks
/speckit.implement
```

### New Workflow (Amplifier Collection)
```bash
# Profile-based workflow
uvx --from git+https://github.com/microsoft/amplifier@next amplifier profile use spec-kit:spec-writer
uvx --from git+https://github.com/microsoft/amplifier@next amplifier run "Create specification with constitutional governance"

uvx --from git+https://github.com/microsoft/amplifier@next amplifier profile use spec-kit:planner
uvx --from git+https://github.com/microsoft/amplifier@next amplifier run "Generate implementation plan"

uvx --from git+https://github.com/microsoft/amplifier@next amplifier profile use spec-kit:implementer
uvx --from git+https://github.com/microsoft/amplifier@next amplifier run "Execute implementation"
```

**Benefits of Amplifier collection**:
- Native agent delegation
- State management across phases
- Cross-collection collaboration (can use with DDD, design-intelligence)
- Event observability
- Richer integration with Amplifier ecosystem

**Original spec-kit remains available** - Use whichever fits your needs.

---

## Advanced Usage

### With DDD Collection

Combine formal specifications with existing codebase integration:

```bash
# Create formal specification (Spec-Kit)
uvx --from git+https://github.com/microsoft/amplifier@next amplifier profile use spec-kit:spec-writer
uvx --from git+https://github.com/microsoft/amplifier@next amplifier run "Create API spec"

# Update existing documentation (DDD)
uvx --from git+https://github.com/microsoft/amplifier@next amplifier profile use amplifier-collection-ddd:documentation
uvx --from git+https://github.com/microsoft/amplifier@next amplifier run "Update docs to reference specs/api.md"

# Implement with integration (DDD)
uvx --from git+https://github.com/microsoft/amplifier@next amplifier profile use amplifier-collection-ddd:implementation
uvx --from git+https://github.com/microsoft/amplifier@next amplifier run "Implement spec with existing codebase"
```

### With Design Intelligence

Combine specifications with design expertise:

```bash
# Design UI (Design Intelligence)
uvx --from git+https://github.com/microsoft/amplifier@next amplifier profile use amplifier-collection-design-intelligence:designer
uvx --from git+https://github.com/microsoft/amplifier@next amplifier run "Design payment UI components"

# Specify API contracts (Spec-Kit)
uvx --from git+https://github.com/microsoft/amplifier@next amplifier profile use spec-kit:spec-writer
uvx --from git+https://github.com/microsoft/amplifier@next amplifier run "Create API spec for payment UI"
```

---

## Installation Methods

### Via Amplifier (Recommended)

```bash
uvx --from git+https://github.com/microsoft/amplifier@next amplifier collection add git+https://github.com/robotdad/amplifier-collection-spec-kit@main
```

### Specific Versions

```bash
# Latest release
... amplifier collection add git+https://github.com/robotdad/amplifier-collection-spec-kit@main

# Development version
... amplifier collection add git+https://github.com/robotdad/amplifier-collection-spec-kit@main

# Specific commit
... amplifier collection add git+https://github.com/robotdad/amplifier-collection-spec-kit@abc1234
```

---

## Contributing

Contributions welcome! See [SUPPORT.md](SUPPORT.md) for how to:
- Report issues
- Request features
- Submit pull requests

---

## License

MIT License - See [LICENSE](LICENSE) for details.

---

## Attribution

This collection adapts GitHub's [Spec-Kit](https://github.com/github/spec-kit) methodology for Amplifier's native agent system. Original spec-kit by GitHub, collection adaptation by robotdad.

---

## Related Collections

- **foundation** - Base profiles and shared context (required dependency)
- **developer-expertise** - Additional development agents
- **ddd** - Document-driven development for existing codebases
- **design-intelligence** - Design expertise and methodology

---

**Version**: 1.0.0
**Author**: robotdad
**Repository**: https://github.com/robotdad/amplifier-collection-spec-kit
