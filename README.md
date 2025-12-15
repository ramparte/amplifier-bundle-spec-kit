# Specification-Driven Development Collection

> Transform requirements into implementation through formal specifications with constitutional governance

**Version**: 1.1.0  
**Author**: robotdad  
**Repository**: https://github.com/robotdad/amplifier-collection-spec-kit

---

## Table of Contents

- [What is Specification-Driven Development?](#what-is-specification-driven-development)
- [What This Collection Provides](#what-this-collection-provides)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Complete Workflow Guide](#complete-workflow-guide)
- [For Spec-Kit Users](#for-spec-kit-users)
- [For Amplifier Users](#for-amplifier-users)
- [Constitutional Principles](#constitutional-principles)
- [Resources](#resources)
- [Examples](#examples)
- [Troubleshooting](#troubleshooting)
- [Advanced Usage](#advanced-usage)
- [Contributing](#contributing)

---

## What is Specification-Driven Development?

**Specification-Driven Development (SDD)** inverts the traditional software development model:

### Traditional Development
```
Idea → Code → Tests → Documentation → (Specs drift from reality)
```

### Specification-Driven Development
```
Idea → Formal Specification → Validation → Plan → Implementation
         (Source of Truth)      (Gates)    (Blueprint)  (Generated)
```

**Core Principle**: "Specifications ARE the source. Code is generated from specifications."

### Why SDD?

- **Eliminates drift**: Specs don't fall out of sync because code is regenerated from specs
- **AI-optimized**: LLMs excel at generating code from precise specifications
- **Quality gates**: Constitutional principles enforced before implementation
- **Team alignment**: Shared understanding before writing code
- **Regeneratable**: Rebuild any module from its specification

---

## What This Collection Provides

The **Spec-Kit Collection** brings GitHub's Specification-Driven Development methodology to Amplifier as native agents and workflows:

### 8 Specialized Agents

Each agent is an expert in a specific SDD phase:

| Agent | Role | Phase |
|-------|------|-------|
| **constitutional-guardian** | Enforces governance rules across all phases | All |
| **spec-smith** | Creates formal specifications from requirements | Specify |
| **spec-critic** | Reviews and validates specifications for quality | Specify |
| **requirement-clarifier** | Resolves ambiguities through targeted questioning | Clarify |
| **research-architect** | Evaluates technology options with trade-off analysis | Plan |
| **plan-architect** | Creates comprehensive implementation plans | Plan |
| **task-decomposer** | Breaks plans into atomic, executable tasks | Plan |
| **implementation-guide** | Guides implementation with TDD enforcement | Implement |

### 3 Phase-Specific Profiles

Pre-configured capability sets for each workflow phase:

- **spec-writer**: Specification creation and validation
- **planner**: Implementation planning with research
- **implementer**: Execution and verification

### Constitutional Governance

8 explicit quality principles enforced throughout:
1. Library-First Principle
2. CLI Interface Requirement
3. Test-First Development (NON-NEGOTIABLE)
4. Integration Testing Priority
5. Simplicity Gates
6. Anti-Abstraction Rule
7. Observability Requirement
8. Versioning & Breaking Changes

### Rich Template System

Templates that constrain LLM behavior for consistency:
- **Specification templates**: Feature specs, API contracts
- **Planning templates**: Research reports, data models, quickstart guides, API contracts
- **Implementation templates**: Task breakdowns with dependencies

### Complete Examples

Real-world examples showing the full workflow:
- **Specifications**: Authentication API, Payment Flow, User Profile
- **Plans**: Implementation plans with research and architecture
- **Tasks**: Detailed task breakdowns with TDD ordering

---

## Installation

### Prerequisites

- Python 3.11+ with `uv` or `uvx`
- Git
- Amplifier installed (or use `uvx` for one-time execution)

### Install Collection

```bash
# Via uvx (recommended - no installation needed)
uvx --from git+https://github.com/microsoft/amplifier@next amplifier collection add git+https://github.com/robotdad/amplifier-collection-spec-kit@main

# Or install Amplifier first, then add collection
uv tool install git+https://github.com/microsoft/amplifier@next
amplifier collection add git+https://github.com/robotdad/amplifier-collection-spec-kit@main
```

### Verify Installation

```bash
amplifier collection list
# Should show: spec-kit (1.1.0)

amplifier agents list
# Should show 8 spec-kit agents

amplifier profile list
# Should show: spec-kit:spec-writer, spec-kit:planner, spec-kit:implementer
```

---

## Quick Start

### 5-Minute Example: Create an API Specification

```bash
# 1. Activate specification profile
amplifier profile use spec-kit:spec-writer

# 2. Create specification
amplifier run "Create API specification for user authentication with JWT tokens"

# Output: specs/001-user-auth/spec.md with:
# - User stories (P1, P2, P3)
# - Functional requirements
# - Success criteria
# - Constitutional compliance check

# 3. Review and approve specification
cat specs/001-user-auth/spec.md

# 4. Create implementation plan
amplifier profile use spec-kit:planner
amplifier run "Create implementation plan for specs/001-user-auth/spec.md"

# Output: Multiple planning artifacts:
# - research.md (technology evaluation)
# - plan.md (implementation blueprint)
# - data-model.md (database schema)
# - contracts/ (API specifications)
# - tasks.md (executable task breakdown)

# 5. Implement
amplifier profile use spec-kit:implementer
amplifier run "Implement tasks from specs/001-user-auth/tasks.md"
```

---

## Complete Workflow Guide

### Phase 1: Specification

**Goal**: Transform requirements into formal, unambiguous specifications.

#### Step 1.1: Create Specification

```bash
amplifier profile use spec-kit:spec-writer
amplifier run "Create specification for [feature description]"
```

**What happens**:
- `spec-smith` agent interviews you for requirements
- Creates `specs/NNN-feature-name/spec.md`
- Applies specification template
- Validates against constitutional principles

**Output structure**:
```markdown
# Feature Specification: [Feature Name]

## Feature Overview
- What, Why, Scope

## User Scenarios & Testing
- User Story 1 (Priority P1)
- User Story 2 (Priority P2)
- etc.

## Functional Requirements
- FR-001: System MUST...
- FR-002: System MUST...

## Success Criteria
- SC-001: Measurable outcome
- SC-002: Measurable outcome

## Constitutional Compliance Check
```

#### Step 1.2: Review Specification

```bash
amplifier run "Review specs/NNN-feature-name/spec.md for quality and completeness"
```

**What happens**:
- `spec-critic` agent scores specification (38-point system)
- Identifies ambiguities
- Suggests improvements
- Validates constitutional compliance

**Quality threshold**: 80+ score to proceed

#### Step 1.3: Clarify Ambiguities (if needed)

```bash
amplifier run "Clarify ambiguities in specs/NNN-feature-name/spec.md"
```

**What happens**:
- `requirement-clarifier` agent asks targeted questions
- Resolves `[NEEDS CLARIFICATION]` markers
- Updates specification with answers

**Limit**: Maximum 3 clarification markers allowed

---

### Phase 2: Planning

**Goal**: Create comprehensive implementation plan with research, architecture, and tasks.

#### Step 2.1: Research Technology Options

```bash
amplifier profile use spec-kit:planner
amplifier run "Research technology options for specs/NNN-feature-name/spec.md"
```

**What happens**:
- `research-architect` agent evaluates options
- Creates `specs/NNN-feature-name/research.md`
- Compares alternatives with pros/cons
- Makes recommendations
- Validates constitutional compliance

**Output**: Research report with technology decision points (TDPs)

#### Step 2.2: Create Implementation Plan

```bash
amplifier run "Create implementation plan for specs/NNN-feature-name/spec.md"
```

**What happens**:
- `plan-architect` agent coordinates planning
- Creates multiple artifacts:
  - `plan.md` - Master implementation plan
  - `data-model.md` - Database schema and entities
  - `quickstart.md` - Validation scenarios
  - `contracts/` - API/interface specifications

**Planning phases**:
- Phase 0: Research (technology evaluation)
- Phase 1: Architecture (data models, contracts)
- Phase 2: Implementation plan (project structure, sequencing)

#### Step 2.3: Break into Tasks

```bash
amplifier run "Create task breakdown for specs/NNN-feature-name/plan.md"
```

**What happens**:
- `task-decomposer` agent creates `specs/NNN-feature-name/tasks.md`
- Atomic tasks (2-4 hours each)
- Dependencies explicitly marked
- Parallel tasks marked with `[P]`
- TDD ordering (tests before implementation)

**Output**: Task list organized by user story with checkpoints

---

### Phase 3: Implementation

**Goal**: Execute implementation systematically with continuous validation.

#### Step 3.1: Execute Tasks

```bash
amplifier profile use spec-kit:implementer
amplifier run "Implement specs/NNN-feature-name/tasks.md"
```

**What happens**:
- `implementation-guide` agent executes tasks sequentially
- Enforces TDD (Red-Green-Refactor)
- Validates against specification
- Checks constitutional compliance
- Marks tasks as completed

#### Step 3.2: Validate Implementation

```bash
amplifier run "Validate implementation against specs/NNN-feature-name/spec.md"
```

**What happens**:
- Runs all quickstart scenarios
- Verifies success criteria met
- Checks constitutional compliance
- Confirms all tests pass

**Acceptance criteria**:
- All P1 user stories implemented
- All success criteria met
- All tests passing
- Constitutional principles upheld

---

## For Spec-Kit Users

If you're using the [original GitHub spec-kit](https://github.com/github/spec-kit), here's how to transition.

### Command Mapping

| Original Spec-Kit | Amplifier Collection |
|-------------------|---------------------|
| `specify init <project>` | `amplifier collection add spec-kit` |
| `/speckit.constitution` | (Automatically loaded from context) |
| `/speckit.specify` | `amplifier profile use spec-kit:spec-writer` + `run` |
| `/speckit.clarify` | `amplifier run "Clarify ambiguities in spec.md"` |
| `/speckit.plan` | `amplifier profile use spec-kit:planner` + `run` |
| `/speckit.tasks` | (Included in planning phase) |
| `/speckit.implement` | `amplifier profile use spec-kit:implementer` + `run` |

### Key Differences

#### Original Spec-Kit
- **CLI tool**: Standalone `specify` command
- **Slash commands**: In AI assistant chat
- **Single session**: One command at a time
- **Script-based**: Bash/PowerShell automation
- **15+ AI tools**: Works with many assistants

#### Amplifier Collection
- **Native agents**: Purpose-built AI personas
- **Profile-based**: Context switching via profiles
- **Multi-session**: State management across phases
- **Agent delegation**: Specialized agents for each task
- **Amplifier ecosystem**: Integrates with other collections

### Benefits of Amplifier Collection

1. **Agent Specialization**: 8 expert agents vs generic AI
2. **State Management**: Automatic context across phases
3. **Cross-Collection**: Combine with DDD, Design Intelligence, etc.
4. **Event Observability**: Built-in logging and tracing
5. **Testing Infrastructure**: Validation framework included

### When to Use Original vs Collection

**Use Original Spec-Kit**:
- You use multiple AI assistants (Claude, Cursor, Copilot, etc.)
- You prefer slash commands in chat
- You want standalone CLI tool
- You don't use Amplifier

**Use Amplifier Collection**:
- You use Amplifier as your development platform
- You want agent specialization
- You need cross-collection workflows
- You want state management across sessions

### Migration Path

```bash
# 1. Keep existing specifications
# Your specs/ directory is compatible!

# 2. Install Amplifier collection
amplifier collection add git+https://github.com/robotdad/amplifier-collection-spec-kit@main

# 3. Use profiles instead of slash commands
amplifier profile use spec-kit:planner
amplifier run "Create plan for specs/existing-feature/spec.md"

# 4. Continue from any phase
# Amplifier collection can pick up where original spec-kit left off
```

**Both tools are maintained**: Use whichever fits your workflow!

---

## For Amplifier Users

If you're new to Amplifier or want to add SDD to your workflow:

### Why Add Spec-Kit Collection?

**Before Spec-Kit**:
- Ad-hoc specifications (if any)
- Requirements in tickets/docs
- Specifications drift from code
- Unclear quality standards
- Inconsistent approaches

**After Spec-Kit**:
- Formal specification workflow
- Constitutional governance
- Template-driven consistency
- Validated before implementation
- Regeneratable from specs

### How It Fits Amplifier

Spec-Kit is one of many Amplifier collections:

```
Foundation (required base)
  ↓
Developer Expertise (zen-architect, bug-hunter, etc.)
  ↓
Spec-Kit (specification-driven workflow) ← You are here
DDD (document-driven development)
Design Intelligence (design expertise)
Toolkit (utility tools)
```

### Integration Patterns

#### Pattern 1: Spec-Kit Only (Greenfield)

```bash
# New feature, no existing code
amplifier profile use spec-kit:spec-writer
amplifier run "Create specification for new payment API"
# → Follow full SDD workflow
```

#### Pattern 2: Spec-Kit + DDD (Existing Codebase)

```bash
# Formal spec for existing system
amplifier profile use spec-kit:spec-writer
amplifier run "Create spec for existing authentication system"

# Update code to match spec
amplifier profile use ddd:implementation
amplifier run "Refactor auth to match spec"
```

#### Pattern 3: Spec-Kit + Design Intelligence (UI/UX)

```bash
# Design first
amplifier profile use design-intelligence:designer
amplifier run "Design payment flow UI"

# Then specify API
amplifier profile use spec-kit:spec-writer
amplifier run "Create API spec for payment UI"
```

### Best Practices

1. **Start with Constitution**: Define your governance rules first
2. **One Spec Per Feature**: Keep specifications focused and bounded
3. **Validate Before Plan**: Don't plan unclear specifications
4. **Follow TDD**: Tests before implementation (NON-NEGOTIABLE)
5. **Use Quickstart**: Validate scenarios before declaring done

### Common Questions

**Q: Do I need to use all 8 agents?**  
A: No! Profiles activate relevant agents automatically. You just switch profiles.

**Q: Can I skip phases?**  
A: Not recommended. Each phase builds on the previous. Skipping leads to problems.

**Q: What if I have existing specifications?**  
A: Great! Use planning profile to create implementation plan from existing spec.

**Q: How long does the full workflow take?**  
A: Depends on feature complexity. Simple API: 2-4 hours. Complex system: 1-2 days.

**Q: Can I use my own templates?**  
A: Yes! Copy templates to your project and modify. Agents will use project templates over collection templates.

---

## Constitutional Principles

The collection enforces 8 core principles throughout development:

### Article I: Library-First Principle

**Rule**: Every feature MUST be implemented as a library first.

**Why**: Libraries are composable, testable, and reusable. UI/CLI are thin wrappers.

**Validation**:
```python
# ✅ Good: Library with programmatic API
from payment_lib import process_payment
result = process_payment(amount=100, currency="USD")

# ❌ Bad: Monolithic application without library interface
```

### Article II: CLI Interface Requirement

**Rule**: All libraries MUST provide CLI with text input/output.

**Why**: Text-based interfaces enable automation, testing, and composition.

**Validation**:
```bash
# ✅ Good: CLI with text I/O
payment-cli process --amount 100 --currency USD
{"status": "success", "transaction_id": "txn_123"}

# ❌ Bad: GUI-only interface
```

### Article III: Test-First Development (NON-NEGOTIABLE)

**Rule**: ALL implementation MUST follow strict TDD (Red-Green-Refactor).

**Why**: Tests drive design. Code written after tests has better interfaces.

**Validation**:
```bash
# ✅ Good: Test fails first
git log:
- Add integration test (FAILING)
- Implement feature (tests now pass)

# ❌ Bad: Implementation before tests
git log:
- Implement feature
- Add tests after the fact
```

### Article IV: Integration Testing Priority

**Rule**: Prefer real dependencies over mocks in tests.

**Why**: Integration tests catch real issues. Mocks give false confidence.

**Validation**:
```python
# ✅ Good: Real database
def test_payment():
    db = TestDatabase()  # Real PostgreSQL
    result = process_payment(db, ...)

# ❌ Bad: All mocks
def test_payment():
    mock_db = Mock()
    mock_stripe = Mock()
    result = process_payment(mock_db, mock_stripe, ...)
```

### Article V: Simplicity Gates

**Rule**: Maximum 3 projects initially. Justify all complexity.

**Why**: Complexity kills velocity. Start simple, add complexity only when proven necessary.

**Validation**:
- 1 project: ✅ Excellent
- 2 projects: ✅ Good (justify in plan)
- 3 projects: ⚠️ Acceptable (strong justification required)
- 4+ projects: ❌ Violation (needs constitution amendment)

### Article VI: Anti-Abstraction Rule

**Rule**: Use frameworks directly. No wrapper layers.

**Why**: Abstraction layers add complexity without flexibility. Framework migrations are rare.

**Validation**:
```python
# ✅ Good: Direct framework usage
from fastapi import FastAPI
app = FastAPI()

# ❌ Bad: Custom wrapper
from my_web_framework import MyFramework
app = MyFramework(FastAPI())  # Unnecessary layer
```

### Article VII: Observability Requirement

**Rule**: All operations MUST be observable (logging, metrics, tracing).

**Why**: Can't debug what you can't see. Observability is not optional.

**Validation**:
```python
# ✅ Good: Structured logging
logger.info("Processing payment", extra={
    "amount": amount,
    "user_id": user_id,
    "trace_id": trace_id
})

# ❌ Bad: No logging
process_payment(amount)  # Silent operation
```

### Article VIII: Versioning & Breaking Changes

**Rule**: API contracts are versioned. Breaking changes documented.

**Why**: Consumers need stability and migration guidance.

**Validation**:
- API version in URL: `/api/v1/payments`
- Breaking changes: 6 months deprecation notice
- Migration guides provided

**Full Details**: See `context/constitution/core-rules.md`

---

## Resources

### Profiles

| Profile | Purpose | Active Agents | Temperature |
|---------|---------|---------------|-------------|
| **spec-writer** | Specification creation | constitutional-guardian, spec-smith, spec-critic, requirement-clarifier | 0.3 (precise) |
| **planner** | Implementation planning | constitutional-guardian, research-architect, plan-architect, task-decomposer | 0.4 (balanced) |
| **implementer** | Execution | constitutional-guardian, implementation-guide | 0.4 (balanced) |

### Context Files

**Constitution** (`context/constitution/`):
- `core-rules.md` - 8 fundamental principles (188 lines)
- `spec-requirements.md` - What makes valid specifications (177 lines)
- `quality-standards.md` - Quality thresholds and gates (12KB)
- `anti-patterns.md` - Common mistakes to avoid (20KB)

**Templates** (`context/templates/`):
- **Specification**: `feature-spec.md` (115 lines)
- **Planning**: `plan-template.md` (104 lines), `research-template.md` (6KB), `data-model-template.md` (10KB), `quickstart-template.md` (9KB), `contract-template.md` (14KB)
- **Implementation**: `task-template.md` (9KB)

**Examples** (`context/examples/`):
- **Specifications**: `auth-api-example.md`, `payment-flow-example.md` (13KB), `user-profile-example.md` (15KB)
- **Plans**: `payment-flow-plan.md` (13KB)
- **Tasks**: `payment-flow-tasks.md` (20KB) - Complete task breakdown with 70 tasks

---

## Examples

### Example 1: Authentication API (Simple)

**Specification**: `context/examples/specifications/auth-api-example.md`

**What it shows**:
- JWT authentication flow
- Priority 1 (P1) user stories
- Functional requirements
- Success criteria
- Constitutional compliance

**Time to implement**: ~6 hours

### Example 2: Payment Flow (Complex)

**Specification**: `context/examples/specifications/payment-flow-example.md`  
**Plan**: `context/examples/plans/payment-flow-plan.md`  
**Tasks**: `context/examples/tasks/payment-flow-tasks.md`

**What it shows**:
- Complete SDD workflow (spec → plan → tasks)
- External integration (Stripe)
- Webhook handling
- Refund processing
- 70-task breakdown
- TDD ordering

**Time to implement**: ~12 days

### Example 3: User Profile (Medium)

**Specification**: `context/examples/specifications/user-profile-example.md`

**What it shows**:
- CRUD operations
- File upload (avatars)
- Account management
- Email preferences
- Account deletion with grace period

**Time to implement**: ~8 hours

### How to Use Examples

```bash
# Copy example specification
cp context/examples/specifications/payment-flow-example.md specs/002-payment-flow/spec.md

# Generate plan from example spec
amplifier profile use spec-kit:planner
amplifier run "Create implementation plan for specs/002-payment-flow/spec.md"

# Or study example plan
cat context/examples/plans/payment-flow-plan.md

# Or study example tasks
cat context/examples/tasks/payment-flow-tasks.md
```

---

## Troubleshooting

### Issue: Agent doesn't follow template

**Symptom**: Specification doesn't match template structure.

**Solution**:
```bash
# Explicitly reference template
amplifier run "Create specification using template @spec-kit:context/templates/specification/feature-spec.md"
```

### Issue: Constitutional violation not caught

**Symptom**: Implementation violates principles but no error raised.

**Solution**:
```bash
# Manually invoke constitutional guardian
amplifier run "Review specs/NNN-feature/spec.md for constitutional compliance"
```

### Issue: Clarification loop (too many questions)

**Symptom**: Agent asks endless clarification questions.

**Solution**: Maximum 3 clarifications enforced in template. If loop occurs:
```bash
# Be more specific in initial request
amplifier run "Create specification for JWT authentication with 24-hour token expiry, refresh tokens, and bcrypt password hashing"
```

### Issue: Task breakdown too granular/coarse

**Symptom**: Tasks are too small (30 min) or too large (3 days).

**Solution**:
```bash
# Specify task granularity
amplifier run "Break plan into tasks, each 2-4 hours of work"
```

### Issue: Tests not written first

**Symptom**: Implementation before tests (violates Article III).

**Solution**: Task template enforces test ordering. If violated:
```bash
# Explicitly request TDD
amplifier run "Implement with strict TDD: write tests first, verify they fail, then implement"
```

### Issue: Agent creates wrapper layers

**Symptom**: Custom abstractions over frameworks (violates Article VI).

**Solution**:
```bash
# Explicitly reference principle
amplifier run "Implement using Stripe SDK directly per Anti-Abstraction Rule (Article VI)"
```

### Issue: Can't find template files

**Symptom**: Error: "Template not found @spec-kit:context/templates/..."

**Solution**:
```bash
# Verify collection installed
amplifier collection list | grep spec-kit

# Reinstall if needed
amplifier collection remove spec-kit
amplifier collection add git+https://github.com/robotdad/amplifier-collection-spec-kit@main
```

### Getting Help

1. **Check Examples**: `context/examples/` for reference implementations
2. **Check Templates**: `context/templates/` for structure
3. **Check Constitution**: `context/constitution/` for principles
4. **Check Anti-Patterns**: `context/constitution/anti-patterns.md` for common mistakes
5. **Open Issue**: https://github.com/robotdad/amplifier-collection-spec-kit/issues

---

## Advanced Usage

### Custom Templates

Override collection templates with project-specific versions:

```bash
# Create project template directory
mkdir -p .amplifier/spec-kit-templates/

# Copy and modify template
cp context/templates/specification/feature-spec.md .amplifier/spec-kit-templates/custom-spec.md
# Edit .amplifier/spec-kit-templates/custom-spec.md

# Use custom template
amplifier run "Create specification using template @project:.amplifier/spec-kit-templates/custom-spec.md"
```

### Custom Constitution

Extend constitutional principles for your project:

```bash
# Create project constitution
mkdir -p .amplifier/constitution/
cat > .amplifier/constitution/project-rules.md <<EOF
# Project-Specific Rules

## Article IX: Database Versioning
All database changes MUST use migrations. No manual schema changes.

## Article X: API Deprecation
APIs MUST maintain backward compatibility for 12 months.
EOF

# Reference in specifications
amplifier run "Create specification with constitutional compliance per @project:.amplifier/constitution/"
```

### Combining with Other Collections

#### With DDD Collection

```bash
# 1. Create formal spec (Spec-Kit)
amplifier profile use spec-kit:spec-writer
amplifier run "Create API specification for existing user service"

# 2. Update existing code (DDD)
amplifier profile use ddd:implementation
amplifier run "Refactor existing user service to match specs/user-service.md"

# 3. Generate documentation (DDD)
amplifier profile use ddd:documentation
amplifier run "Generate API docs from specs/user-service.md"
```

#### With Design Intelligence

```bash
# 1. Design UI components (Design Intelligence)
amplifier profile use design-intelligence:designer
amplifier run "Design checkout flow UI components"

# 2. Specify backend API (Spec-Kit)
amplifier profile use spec-kit:spec-writer
amplifier run "Create API specification supporting checkout UI"

# 3. Plan implementation (Spec-Kit)
amplifier profile use spec-kit:planner
amplifier run "Create implementation plan for checkout API"
```

### Parallel Task Execution

Task breakdowns mark parallel tasks with `[P]`:

```markdown
- [ ] T001 [P] Create User model
- [ ] T002 [P] Create Payment model
- [ ] T003 [P] Create Subscription model
- [ ] T004 Implement UserService (depends on T001)
```

Execute parallel tasks:
```bash
# In separate terminals or CI pipeline
amplifier run "Implement task T001 from specs/feature/tasks.md"
amplifier run "Implement task T002 from specs/feature/tasks.md"
amplifier run "Implement task T003 from specs/feature/tasks.md"
```

### Continuous Integration

Integrate SDD workflow into CI/CD:

```yaml
# .github/workflows/spec-validation.yml
name: Specification Validation

on: [pull_request]

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Install Amplifier
        run: uvx --from git+https://github.com/microsoft/amplifier@next amplifier collection add git+https://github.com/robotdad/amplifier-collection-spec-kit@main
      
      - name: Validate Specifications
        run: |
          amplifier profile use spec-kit:spec-writer
          amplifier run "Review all specifications in specs/ for constitutional compliance"
```

---

## Contributing

Contributions welcome! Here's how to help:

### Report Issues

https://github.com/robotdad/amplifier-collection-spec-kit/issues

Include:
- What you were trying to do
- What happened
- What you expected
- Relevant logs/error messages

### Suggest Improvements

- New agents for additional phases
- Enhanced templates
- Additional examples
- Constitutional principles
- Documentation improvements

### Submit Pull Requests

1. Fork the repository
2. Create feature branch
3. Make changes
4. Add tests if applicable
5. Update documentation
6. Submit PR

See [SUPPORT.md](SUPPORT.md) for details.

---

## Comparison Matrix

### Spec-Kit vs Traditional Development

| Aspect | Traditional | Spec-Kit |
|--------|-------------|----------|
| **Requirements** | Tickets, docs | Formal specifications |
| **Validation** | After code | Before code |
| **Drift** | Inevitable | Prevented |
| **Quality Gates** | Informal | Constitutional |
| **AI Optimization** | Ad-hoc prompts | Template-constrained |
| **Regeneration** | Hard | Easy |
| **Team Alignment** | Variable | Guaranteed |

### Original Spec-Kit vs Amplifier Collection

| Feature | Original CLI | Amplifier Collection |
|---------|-------------|---------------------|
| **AI Support** | 15+ assistants | Amplifier ecosystem |
| **Execution** | Slash commands | Native agents |
| **Specialization** | Generic AI | 8 expert agents |
| **State** | Single session | Multi-session |
| **Integration** | Standalone | Cross-collection |
| **Observability** | None | Built-in |
| **Testing** | Manual | Framework |

---

## License

MIT License - See [LICENSE](LICENSE) for details.

---

## Attribution

This collection adapts GitHub's [Spec-Kit](https://github.com/github/spec-kit) methodology for Amplifier's native agent system.

**Original Spec-Kit**: Created by GitHub  
**Amplifier Collection**: Adapted by robotdad

Both implementations are maintained and compatible. Use whichever fits your workflow!

---

## Related Projects

### Amplifier Ecosystem

- **amplifier** - Core platform: https://github.com/microsoft/amplifier
- **foundation** - Base profiles and context (required dependency)
- **developer-expertise** - Development agents (zen-architect, bug-hunter, etc.)

### Other Collections

- **ddd** - Document-driven development for existing codebases
- **design-intelligence** - Design expertise and methodology
- **toolkit** - Utility tools and scenario templates

### Original Spec-Kit

- **spec-kit** - GitHub's original CLI tool: https://github.com/github/spec-kit

---

## Version History

- **1.1.0** (2024-01-15): Complete template library, comprehensive examples, enhanced documentation
- **1.0.0** (2024-01-01): Initial release with 8 agents and 3 profiles

---

## Support

- **Documentation**: This README and `context/` files
- **Examples**: `context/examples/` for reference implementations
- **Issues**: https://github.com/robotdad/amplifier-collection-spec-kit/issues
- **Discussions**: https://github.com/robotdad/amplifier-collection-spec-kit/discussions

For general Amplifier support: https://github.com/microsoft/amplifier

---

**Ready to transform requirements into reality? Start with `amplifier profile use spec-kit:spec-writer`!**
