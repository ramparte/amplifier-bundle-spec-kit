# Specification Anti-Patterns

**Version**: 1.0.0  
**Last Updated**: 2024-01-15

This document catalogs common mistakes and anti-patterns encountered in Specification-Driven Development. Learning to recognize these patterns helps avoid them and leads to better specifications, plans, and implementations.

---

## Specification Anti-Patterns

### 🚫 AP-S01: The Novel Specification

**Description**: Specification reads like a novel with excessive backstory, context, and explanations that obscure the actual requirements.

**Example**:
```markdown
## Background
Our company has a long history of authentication challenges dating back to 2015 
when we first implemented user logins. Over the years, we've tried various 
approaches including basic auth, session cookies, and OAuth 1.0. Each had its 
pros and cons. In 2018, we had a security incident that... [continues for 3 pages]

## Requirements
Users should be able to log in.
```

**Why It's Bad**:
- Requirements are buried in narrative
- Wastes reviewer time
- Hard to extract actionable information

**Better Approach**:
- Put extensive context in separate "Background" document
- Specification should be scannable and actionable
- Link to context documents for those who need it

---

### 🚫 AP-S02: Implementation Disguised as Requirements

**Description**: Specification specifies HOW to build instead of WHAT to build.

**Example**:
```markdown
## Requirements
- FR-001: System MUST use FastAPI framework with Pydantic models
- FR-002: Database MUST be PostgreSQL 15 with SQLAlchemy ORM
- FR-003: MUST implement JWT tokens using the jose library
- FR-004: Frontend MUST use React with Redux for state management
```

**Why It's Bad**:
- Locks in technology choices prematurely
- Violates separation between WHAT and HOW
- Prevents evaluation of alternatives
- Makes specification obsolete when technology changes

**Better Approach**:
```markdown
## Requirements
- FR-001: System MUST authenticate users securely
- FR-002: System MUST persist user credentials safely
- FR-003: System MUST maintain user sessions across requests
- FR-004: System MUST provide a responsive user interface

## Success Criteria
- SC-001: Authentication completes in <2 seconds
- SC-002: Credentials are encrypted at rest
- SC-003: Sessions remain valid for 24 hours
- SC-004: UI is usable on mobile devices
```

---

### 🚫 AP-S03: Vague Success Criteria

**Description**: Success criteria use subjective language without measurable outcomes.

**Example**:
```markdown
## Success Criteria
- SC-001: System is fast
- SC-002: UI is intuitive and easy to use
- SC-003: Code is maintainable
- SC-004: Performance is good enough
```

**Why It's Bad**:
- Impossible to verify objectively
- Leads to disagreements about "done"
- Provides no guidance for implementation

**Better Approach**:
```markdown
## Success Criteria
- SC-001: API responds in <100ms for p95 of requests
- SC-002: Users complete first login in <2 minutes without help
- SC-003: New developers can run local environment in <15 minutes
- SC-004: System handles 1000 concurrent users without errors
```

---

### 🚫 AP-S04: The Grab Bag Specification

**Description**: Multiple unrelated features crammed into one specification.

**Example**:
```markdown
# User Management, Reporting, Payment Processing, and Email System

This specification covers user registration, password reset, admin dashboard, 
financial reports, payment gateway integration, subscription billing, email 
templates, and notification system.
```

**Why It's Bad**:
- Impossible to estimate or scope
- Cannot be implemented incrementally
- Violates single responsibility
- Hard to review or approve

**Better Approach**:
- One specification per feature or bounded context
- Multiple specifications can reference each other
- Clear scope boundaries

---

### 🚫 AP-S05: Future-Proofing Overload

**Description**: Specification tries to anticipate every possible future need.

**Example**:
```markdown
## Requirements
- FR-001: System MUST support users, groups, organizations, and departments
- FR-002: MUST support single-factor, two-factor, and three-factor auth
- FR-003: MUST support OAuth 2.0, SAML, LDAP, and custom providers
- FR-004: MUST be deployable on AWS, Azure, GCP, on-prem, and edge devices
- FR-005: MUST support English, Spanish, French, German, Japanese, and Arabic

[Note: We currently have 10 users, all English-speaking]
```

**Why It's Bad**:
- Massive scope creep
- Delays delivery of actual needed features
- Increases complexity unnecessarily
- Most "future needs" never materialize

**Better Approach**:
- Focus on current, validated needs
- Design for extensibility, not every feature
- Add features when actually needed (YAGNI)

---

### 🚫 AP-S06: Death by Edge Cases

**Description**: Specification focuses on edge cases before defining happy path.

**Example**:
```markdown
## User Scenarios

### Edge Case 1: User Enters Invalid Email 57 Times
What if a user enters an invalid email 57 times in a row?

### Edge Case 2: Simultaneous Login from 12 Devices
What if the same user logs in from 12 different devices simultaneously?

### Edge Case 3: Unicode Emoji in Username
What if a username contains 47 different emoji characters?

[No description of normal login flow]
```

**Why It's Bad**:
- Obscures the primary use case
- Analysis paralysis
- Implementation starts with edge cases

**Better Approach**:
- Define happy path first (P1 scenarios)
- Edge cases are P2/P3
- Most edge cases are handled generically

---

### 🚫 AP-S07: The Moving Target

**Description**: Specification constantly changes during implementation.

**Symptoms**:
- "Actually, we also need..."
- "I forgot to mention..."
- "Can we add just one more thing?"
- Specification version 47 during implementation

**Why It's Bad**:
- Destroys estimates and timelines
- Demoralizes team
- Never reaches "done"
- Indicates poor initial analysis

**Better Approach**:
- Freeze specification after approval
- New requirements → new specification
- Clear change control process
- Clarifications are OK, scope changes are not

---

## Planning Anti-Patterns

### 🚫 AP-P01: Research-Free Planning

**Description**: Jumping straight to architecture without researching options.

**Example**:
```markdown
## Technology Decisions
We'll use Framework X because I used it before.
```

**Why It's Bad**:
- Misses better alternatives
- No justification for decisions
- Can't evaluate tradeoffs
- Violates constitutional research requirement

**Better Approach**:
- Always complete Phase 0 research
- Evaluate at least 2 options per decision
- Document pros/cons
- Make informed choices

---

### 🚫 AP-P02: Copy-Paste Architecture

**Description**: Reusing previous project's architecture without considering current needs.

**Example**:
```markdown
## Architecture
We'll use the same architecture as Project X because it worked there.

[Project X was a high-throughput streaming system]
[Current project is a simple CRUD app]
```

**Why It's Bad**:
- Over-engineering for actual needs
- Unnecessary complexity
- Violates simplicity principle

**Better Approach**:
- Start from requirements
- Derive architecture from needs
- Reuse patterns, not wholesale architectures

---

### 🚫 AP-P03: The Abstraction Layer Cake

**Description**: Adding unnecessary abstraction layers "for flexibility".

**Example**:
```
┌─────────────────────────┐
│   HTTP API Layer        │
├─────────────────────────┤
│   API Facade Layer      │
├─────────────────────────┤
│   Service Abstraction   │
├─────────────────────────┤
│   Repository Interface  │
├─────────────────────────┤
│   Data Access Wrapper   │
├─────────────────────────┤
│   ORM Abstraction       │
├─────────────────────────┤
│   Database Driver       │
└─────────────────────────┘
```

**Why It's Bad**:
- Violates Article VI (Anti-Abstraction Rule)
- Every layer adds latency
- Hard to debug (which layer is failing?)
- No actual flexibility gained

**Better Approach**:
```
┌─────────────────────────┐
│   HTTP API (FastAPI)    │
├─────────────────────────┤
│   Business Logic        │
├─────────────────────────┤
│   Database (SQLAlchemy) │
└─────────────────────────┘
```

---

### 🚫 AP-P04: Premature Microservices

**Description**: Breaking system into microservices before understanding boundaries.

**Example**:
```markdown
## Architecture
- User Service (manages users)
- Auth Service (handles authentication)  
- Profile Service (user profiles)
- Preferences Service (user preferences)
- Avatar Service (profile pictures)
- Email Service (sending emails)
- Notification Service (push notifications)

[Total users: 0, Expected users: 100]
```

**Why It's Bad**:
- Violates Article V (Simplicity Gates - max 3 projects)
- Massive operational overhead
- Network latency between services
- Distributed system complexity

**Better Approach**:
- Start monolithic (library + CLI)
- Extract services only when proven necessary
- Justify each additional project

---

### 🚫 AP-P05: The Framework Wrapper

**Description**: Creating abstraction layer over framework "in case we need to switch".

**Example**:
```python
# Custom abstraction layer
class MyHTTPFramework:
    """Abstraction so we can switch from FastAPI to something else easily"""
    def __init__(self, framework: FastAPI):
        self.framework = framework
    
    def route(self, path: str):
        # Wrapper around framework.route
        pass
    
    def middleware(self):
        # Wrapper around framework.middleware
        pass
```

**Why It's Bad**:
- Violates Article VI (Anti-Abstraction Rule)
- Framework switches are extremely rare
- Loses framework features and ecosystem
- Maintenance burden of wrapper layer

**Better Approach**:
- Use framework directly
- If you outgrow it, migrate then (rarely happens)
- Cost of wrapper > cost of potential migration

---

## Task Breakdown Anti-Patterns

### 🚫 AP-T01: The Mega-Task

**Description**: Tasks that take days or weeks to complete.

**Example**:
```markdown
- [ ] T001: Implement authentication feature
- [ ] T002: Build entire API
- [ ] T003: Create frontend
```

**Why It's Bad**:
- Can't track progress granularly
- Tasks stay "in progress" for days
- No early validation

**Better Approach**:
```markdown
- [ ] T001: Create User model
- [ ] T002: Implement user registration endpoint
- [ ] T003: Write integration test for registration
- [ ] T004: Implement login endpoint
```

---

### 🚫 AP-T02: Implementation Before Tests

**Description**: Writing implementation tasks before test tasks.

**Example**:
```markdown
## Phase 1: Implementation
- [ ] T001: Implement login endpoint
- [ ] T002: Implement user service
- [ ] T003: Add database migrations

## Phase 2: Testing
- [ ] T020: Write tests for login
```

**Why It's Bad**:
- Violates Article III (Test-First Development)
- Tests become afterthought
- Hard to retrofit tests later

**Better Approach**:
```markdown
## Phase 1: User Story 1
- [ ] T001 [P]: Contract test for login endpoint
- [ ] T002 [P]: Integration test for login flow
- [ ] T003: Implement login endpoint (depends on T001, T002)
- [ ] T004: Verify tests pass
```

---

### 🚫 AP-T03: Vague Task Descriptions

**Description**: Tasks that don't clearly define what "done" means.

**Example**:
```markdown
- [ ] T001: Fix the thing
- [ ] T002: Make it work
- [ ] T003: Improve performance
- [ ] T004: Add some tests
```

**Why It's Bad**:
- Impossible to estimate
- Unclear when task is complete
- Different interpretations by different people

**Better Approach**:
```markdown
- [ ] T001: Fix login button not responding on mobile Safari
- [ ] T002: Implement JWT token validation middleware
- [ ] T003: Reduce API p95 latency from 500ms to <100ms
- [ ] T004: Add integration tests for all auth endpoints
```

---

## Implementation Anti-Patterns

### 🚫 AP-I01: Test-Last Development

**Description**: Writing tests after implementation is complete.

**Example**:
```bash
$ git log --oneline
abc123 Add tests
def456 Fix bugs found in testing
ghi789 Implement feature
```

**Why It's Bad**:
- Violates Article III (NON-NEGOTIABLE)
- Tests are biased by implementation
- Hard to retrofit test coverage
- Misses design feedback from tests

**Better Approach**:
```bash
$ git log --oneline
abc123 Implement feature (tests passing)
def456 Add integration tests (failing)
ghi789 Add contract tests (failing)
```

---

### 🚫 AP-I02: Mock Everything

**Description**: Using mocks instead of real dependencies in tests.

**Example**:
```python
def test_user_creation():
    # Mock database
    mock_db = Mock()
    # Mock email service
    mock_email = Mock()
    # Mock payment service
    mock_payment = Mock()
    
    # Test with all mocks
    result = create_user(mock_db, mock_email, mock_payment)
```

**Why It's Bad**:
- Violates Article IV (Integration Testing Priority)
- Tests pass but real system fails
- Doesn't test actual integrations
- False confidence

**Better Approach**:
```python
def test_user_creation():
    # Use real test database
    db = TestDatabase()
    # Use real email service in test mode
    email = EmailService(test_mode=True)
    # Only mock external payment service
    mock_payment = Mock()
    
    result = create_user(db, email, mock_payment)
```

---

### 🚫 AP-I03: The God Object

**Description**: Single class/module that does everything.

**Example**:
```python
class UserManager:
    def create_user(self): ...
    def authenticate(self): ...
    def send_email(self): ...
    def process_payment(self): ...
    def generate_pdf(self): ...
    def upload_to_s3(self): ...
    def send_notification(self): ...
    def log_analytics(self): ...
    # ... 50 more methods
```

**Why It's Bad**:
- Hard to test
- Hard to understand
- Hard to modify
- Violates single responsibility

**Better Approach**:
- Separate concerns into focused modules
- Each module does one thing well
- Compose modules to build features

---

### 🚫 AP-I04: Invisible Observability

**Description**: No logging, metrics, or tracing in production.

**Example**:
```python
def process_payment(amount):
    # No logging
    result = payment_gateway.charge(amount)
    return result
```

**Production Debugging**:
```
"The payment failed."
"Which payment?"
"Um... some payment."
"When?"
"Sometime today?"
```

**Why It's Bad**:
- Violates Article VII (Observability Requirement)
- Impossible to debug production issues
- No visibility into system behavior

**Better Approach**:
```python
def process_payment(amount):
    logger.info(f"Processing payment", extra={
        "amount": amount,
        "user_id": user.id,
        "trace_id": trace_id
    })
    
    try:
        result = payment_gateway.charge(amount)
        logger.info(f"Payment successful", extra={
            "transaction_id": result.id,
            "amount": amount
        })
        metrics.increment("payments.success")
        return result
    except PaymentError as e:
        logger.error(f"Payment failed", extra={
            "error": str(e),
            "amount": amount
        })
        metrics.increment("payments.failure")
        raise
```

---

### 🚫 AP-I05: The Magic Number

**Description**: Hard-coded values without explanation.

**Example**:
```python
def retry_request():
    for i in range(7):  # Why 7?
        time.sleep(3.5)  # Why 3.5?
        if request.status == 429:  # What's 429?
            time.sleep(60)  # Why 60?
```

**Why It's Bad**:
- Intent is unclear
- Hard to modify confidently
- No reasoning documented

**Better Approach**:
```python
MAX_RETRIES = 7  # Empirically determined from failure analysis
RETRY_DELAY_SECONDS = 3.5  # Matches server timeout window
HTTP_TOO_MANY_REQUESTS = 429
RATE_LIMIT_COOLDOWN = 60  # Server rate limit window

def retry_request():
    for attempt in range(MAX_RETRIES):
        time.sleep(RETRY_DELAY_SECONDS)
        if request.status == HTTP_TOO_MANY_REQUESTS:
            time.sleep(RATE_LIMIT_COOLDOWN)
```

---

## Process Anti-Patterns

### 🚫 AP-PR01: Skip the Specification

**Description**: Going straight from idea to code.

**Conversation**:
```
PM: "We need user authentication."
Dev: "Got it, I'll start coding."
[3 weeks later]
PM: "This isn't what I wanted."
Dev: "You didn't say that!"
```

**Why It's Bad**:
- Wastes implementation time
- Leads to rework
- Causes friction between teams
- Defeats purpose of SDD

**Better Approach**:
- Always start with specification
- Get specification approved
- Then plan and implement

---

### 🚫 AP-PR02: Specification by Committee

**Description**: Involving everyone in specification details.

**Example**:
```markdown
[Version 47 of specification]
[12 stakeholders with conflicting requirements]
[Meeting #15 to discuss button color]
[Still no approved specification]
```

**Why It's Bad**:
- Analysis paralysis
- Never reaches approval
- Diluted responsibility

**Better Approach**:
- Single owner for specification
- Stakeholder input, not stakeholder consensus
- Time-box specification phase
- Approval by designated authority

---

### 🚫 AP-PR03: The Eternal Beta

**Description**: Never declaring feature "done", always adding "just one more thing".

**Example**:
```markdown
[Month 1] "Feature is 90% done"
[Month 2] "Feature is 90% done"
[Month 3] "Feature is 90% done"
[Month 4] "Feature is 90% done"
```

**Why It's Bad**:
- Never ships
- Scope creep
- Diminishing returns

**Better Approach**:
- Define "done" in specification
- Ship when success criteria met
- New requirements → new specification

---

## How to Use This Document

### For Specification Writers

When writing specifications, review AP-S01 through AP-S07 and ask:
- Am I making any of these mistakes?
- Is my specification actionable and clear?
- Can this be approved and implemented as-is?

### For Plan Architects

When creating plans, review AP-P01 through AP-P05 and ask:
- Am I following constitutional principles?
- Is my architecture as simple as possible?
- Have I justified complexity?

### For Implementers

When writing code, review AP-I01 through AP-I05 and ask:
- Am I following test-first development?
- Is my code observable and maintainable?
- Am I adding unnecessary complexity?

### For Process Facilitators

When managing the SDD workflow, review AP-PR01 through AP-PR03 and ask:
- Are we following the process?
- Are we stuck in any anti-pattern?
- How can we improve?

---

## Contributing to This Document

If you encounter a new anti-pattern:

1. Document the pattern with a clear example
2. Explain why it's problematic
3. Provide a better approach
4. Submit as PR to this document

Anti-patterns should be:
- **Real**: Actually observed, not theoretical
- **Harmful**: Causes concrete problems
- **Recurring**: Seen multiple times
- **Fixable**: Has a known better approach

---

## Summary

Anti-patterns are not personal failures—they're learning opportunities. We all fall into these traps occasionally. The key is:

1. **Recognize** the pattern when it occurs
2. **Understand** why it's problematic
3. **Apply** the better approach
4. **Share** learnings with the team

The goal is continuous improvement, not perfection. Learn from mistakes, adjust, and keep moving forward.
