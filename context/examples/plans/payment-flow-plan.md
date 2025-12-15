# Implementation Plan: Payment Processing Flow

**Branch**: `002-payment-flow` | **Date**: 2024-01-15 | **Spec**: [payment-flow-example.md](../specifications/payment-flow-example.md)  
**Input**: Feature specification from `specs/002-payment-flow/spec.md`

---

## Summary

Implement secure payment processing flow for subscription purchases using Stripe payment gateway. System will handle credit card payments, webhook events, refund processing, and subscription lifecycle management. Core focus on payment success/failure handling and webhook synchronization.

**Technical Approach**: Python-based payment library with FastAPI integration, direct Stripe SDK usage, PostgreSQL for transaction records, async webhook processing.

---

## Technical Context

**Language/Version**: Python 3.11  
**Primary Dependencies**: Stripe Python SDK 7.0+, FastAPI 0.104+, SQLAlchemy 2.0+, Pydantic 2.5+  
**Storage**: PostgreSQL 15 for payment records and subscription state  
**Testing**: pytest + pytest-asyncio + Stripe test mode  
**Target Platform**: Linux server (containerized)  
**Project Type**: Single (library + CLI)  
**Performance Goals**: <5 seconds for payment processing (p95), <60 seconds for webhook processing  
**Constraints**: PCI DSS Level 1 compliance (via Stripe), <100MB memory per request  
**Scale/Scope**: 1000 payments/day initially, scaling to 10K/day

---

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-checked after Phase 1 design.*

### Article I: Library-First Principle
✅ **PASS** - Payment processing implemented as standalone library (`payment_lib`) with programmatic API

### Article II: CLI Interface Requirement
✅ **PASS** - CLI provided for admin operations: `payment-cli process-refund`, `payment-cli webhook-status`

### Article III: Test-First Development (NON-NEGOTIABLE)
✅ **PASS** - TDD workflow planned: contract tests → integration tests → implementation

### Article IV: Integration Testing Priority
✅ **PASS** - Integration tests with Stripe test mode (real API calls), real database

### Article V: Simplicity Gates
✅ **PASS** - Single project, no microservices

**Project Count**: 1 (library + CLI in same package)  
**Justification**: N/A - under limit

### Article VI: Anti-Abstraction Rule
✅ **PASS** - Direct Stripe SDK usage without wrapper layers

### Article VII: Observability Requirement
✅ **PASS** - Structured logging for all payment events, metrics for success/failure rates

### Article VIII: Versioning & Breaking Changes
✅ **PASS** - API contracts versioned (v1), webhook handling versioned

**Overall**: ✅ ALL GATES PASS - Ready for Phase 0 research

---

## Project Structure

### Documentation (this feature)

```text
specs/002-payment-flow/
├── spec.md              # Feature specification
├── plan.md              # This file (master plan)
├── research.md          # Phase 0: Technology evaluation
├── data-model.md        # Phase 1: Database schema design
├── quickstart.md        # Phase 1: Validation scenarios
├── contracts/           # Phase 1: API contracts
│   ├── payment-api.md   # Payment processing API
│   ├── webhook-api.md   # Webhook handler API
│   └── cli.md           # CLI interface
└── tasks.md             # Phase 2: Task breakdown (via task-decomposer)
```

### Source Code (repository root)

```text
src/
├── payment_lib/
│   ├── __init__.py
│   ├── models.py         # Payment, Subscription, PaymentMethod, WebhookEvent
│   ├── payment.py        # Payment processing logic
│   ├── subscription.py   # Subscription management
│   ├── webhook.py        # Webhook handler
│   ├── refund.py         # Refund processing
│   ├── stripe_client.py  # Stripe SDK integration
│   └── exceptions.py     # Payment-specific exceptions
│
├── payment_api/
│   ├── __init__.py
│   ├── main.py           # FastAPI application
│   ├── routes/
│   │   ├── payment.py    # POST /api/v1/payments
│   │   ├── subscription.py  # GET/POST /api/v1/subscriptions
│   │   ├── webhook.py    # POST /api/v1/webhooks/stripe
│   │   └── refund.py     # POST /api/v1/refunds
│   ├── schemas.py        # Pydantic request/response models
│   └── dependencies.py   # FastAPI dependencies
│
└── payment_cli/
    ├── __init__.py
    └── main.py           # Click CLI application

tests/
├── contract/
│   ├── test_payment_api_contract.py
│   ├── test_webhook_contract.py
│   └── test_cli_contract.py
│
├── integration/
│   ├── test_payment_flow.py        # End-to-end payment scenarios
│   ├── test_stripe_integration.py  # Real Stripe API calls (test mode)
│   ├── test_webhook_processing.py  # Webhook event processing
│   └── test_refund_flow.py         # Refund scenarios
│
└── unit/
    ├── test_payment_logic.py       # Payment business logic
    ├── test_subscription_logic.py  # Subscription state management
    └── test_idempotency.py         # Duplicate prevention

alembic/
└── versions/
    └── 001_create_payment_tables.py
```

**Structure Decision**: Single project with library, API, and CLI components. Library is core (can be used independently), API is FastAPI wrapper, CLI is admin tool. All in same repository for simplicity.

---

## Phase 0: Research Report Summary

**Full Report**: See `specs/002-payment-flow/research.md`

### Key Technology Decisions

**TDP-001: Payment Gateway Selection**
- **Chosen**: Stripe
- **Rationale**: Best-in-class developer experience, handles PCI compliance, excellent Python SDK, comprehensive webhook system, test mode for integration tests
- **Alternatives Evaluated**: Square (less webhook flexibility), Braintree (more complex API)

**TDP-002: Database for Transaction Records**
- **Chosen**: PostgreSQL 15
- **Rationale**: ACID transactions critical for payments, JSON columns for flexible webhook payloads, mature Python support (SQLAlchemy)
- **Alternatives Evaluated**: MongoDB (eventual consistency risky for payments)

**TDP-003: Async Processing for Webhooks**
- **Chosen**: Async Python with FastAPI background tasks
- **Rationale**: Webhook endpoint must respond quickly (<5s), actual processing can be async, avoids queue infrastructure initially
- **Alternatives Evaluated**: Celery (overkill for initial scale), Lambda functions (vendor lock-in)

**TDP-004: Idempotency Strategy**
- **Chosen**: Database unique constraint on idempotency_key + application-level checks
- **Rationale**: Prevents duplicate charges at multiple levels, simple to implement
- **Alternatives Evaluated**: Redis-based locking (adds dependency)

### Constitutional Compliance

All research decisions align with constitutional principles:
- Direct Stripe SDK usage (Article VI)
- Integration tests with real Stripe API (Article IV)
- Simple async approach without queue (Article V)
- Observable via structured logging (Article VII)

---

## Phase 1: Architecture & Data Design

### Data Model Summary

**Full Data Model**: See `specs/002-payment-flow/data-model.md`

**Key Entities**:

1. **Payment**
   - Stores payment attempts and results
   - Links to User, Subscription, PaymentMethod
   - Tracks Stripe transaction ID for reconciliation
   - Idempotency key for duplicate prevention

2. **Subscription**
   - Tracks subscription lifecycle (active, past_due, cancelled, expired)
   - Links to User and current PaymentMethod
   - Stores billing dates for renewal scheduling

3. **PaymentMethod**
   - Stores tokenized card info (via Stripe)
   - Never stores raw card numbers (PCI compliance)
   - Tracks card brand and last 4 digits for display

4. **WebhookEvent**
   - Audit trail of all Stripe webhooks
   - Idempotent processing (duplicate webhooks handled safely)
   - Signature verification results logged

**Relationships**:
```
User (1) ──< (many) Payment
User (1) ──< (many) Subscription
User (1) ──< (many) PaymentMethod
Subscription (many) >── (1) PaymentMethod
Payment (many) >── (1) PaymentMethod
Payment (many) >── (1) Subscription
```

### API Contracts Summary

**Full Contracts**: See `specs/002-payment-flow/contracts/`

**Primary Endpoints**:

1. **POST /api/v1/payments** - Process subscription payment
   - Input: user_id, plan_id, payment_method_id, idempotency_key
   - Output: payment_id, status, subscription_id
   - Handles 3D Secure redirects

2. **POST /api/v1/webhooks/stripe** - Receive Stripe webhooks
   - Input: Stripe webhook payload + signature
   - Output: 200 OK (immediate response)
   - Async processing of event

3. **POST /api/v1/refunds** - Issue refund (admin only)
   - Input: payment_id, amount (optional for partial)
   - Output: refund_id, status

**CLI Commands**:
- `payment-cli process-refund <payment-id> [--amount AMOUNT]`
- `payment-cli webhook-status [--pending] [--failed]`
- `payment-cli subscription-info <user-id>`

### Quickstart Scenarios Summary

**Full Quickstart**: See `specs/002-payment-flow/quickstart.md`

**Key Validation Scenarios**:
1. Successful payment with test card
2. Declined payment handling
3. 3D Secure authentication flow
4. Webhook event processing
5. Refund processing

---

## Phase 2: Implementation Plan

### Implementation Phases

**Phase 0: Setup** (Day 1)
- Database schema and migrations
- Stripe test account configuration
- Project structure scaffolding

**Phase 1: Core Payment Processing** (Days 2-4)
- Payment model and database integration
- Stripe API integration for charges
- Idempotency handling
- 3D Secure support

**Phase 2: Subscription Management** (Days 5-6)
- Subscription model and state machine
- Subscription creation on successful payment
- Subscription status tracking

**Phase 3: Webhook Processing** (Days 7-8)
- Webhook endpoint with signature verification
- Event processing logic
- Idempotent webhook handling
- Subscription sync from webhooks

**Phase 4: Refund Processing** (Day 9)
- Refund API and logic
- Subscription cancellation on refund
- Admin CLI for refunds

**Phase 5: Error Handling & Edge Cases** (Day 10)
- Comprehensive error handling
- Rate limiting
- Timeout handling
- Edge case coverage

**Phase 6: Testing & Validation** (Days 11-12)
- Contract tests (all endpoints)
- Integration tests (Stripe test mode)
- Quickstart validation
- Performance testing

### Dependencies & Sequencing

**Critical Path**:
```
Setup → Payment Processing → Subscription Management → Webhook Processing → Refunds → Testing
```

**Parallel Tracks**:
- CLI development can happen in parallel with API development
- Documentation can be written while implementation progresses

### Risk Mitigation

**Risk 1**: Stripe API changes
- **Mitigation**: Pin Stripe SDK version, monitor changelog, test mode catches breaking changes

**Risk 2**: Webhook replay attacks
- **Mitigation**: Verify Stripe signature, check processed status in database

**Risk 3**: Race conditions in webhook processing
- **Mitigation**: Database transactions, idempotency keys, timestamp-based ordering

**Risk 4**: Payment failure edge cases
- **Mitigation**: Comprehensive test suite with Stripe test cards, error scenario testing

---

## Complexity Tracking

> **Fill ONLY if Constitution Check has violations that must be justified**

No violations - all constitutional gates pass.

---

## Implementation Readiness

### Prerequisites Checklist

- [x] Specification approved
- [x] Research completed
- [x] Technology decisions made
- [x] Data model designed
- [x] API contracts defined
- [x] Quickstart scenarios documented
- [x] Constitutional compliance verified
- [x] Risks identified and mitigated

### Ready to Implement

✅ **YES** - All planning phases complete. Implementation can begin.

**Next Step**: Delegate to task-decomposer agent to create detailed task breakdown in `specs/002-payment-flow/tasks.md`

---

## Appendix A: Stripe Test Cards

For integration testing:

| Card Number | Scenario |
|-------------|----------|
| 4242424242424242 | Success |
| 4000000000000002 | Declined |
| 4000000000003220 | 3D Secure required |
| 4000000000009995 | Insufficient funds |
| 4000000000000069 | Expired card |

**Webhook Testing**: Use Stripe CLI for local webhook testing
```bash
stripe listen --forward-to localhost:8000/api/v1/webhooks/stripe
stripe trigger charge.succeeded
```

---

## Appendix B: Key Configuration

**Environment Variables Needed**:
```bash
STRIPE_API_KEY=sk_test_...           # Stripe secret key (test mode)
STRIPE_WEBHOOK_SECRET=whsec_...      # Webhook signing secret
DATABASE_URL=postgresql://...         # Database connection
API_BASE_URL=https://api.example.com # For 3D Secure redirects
```

---

## Approval

**Plan Status**: Approved  
**Approved By**: Technical Lead  
**Approval Date**: 2024-01-15

**Next Step**: Create task breakdown (Phase 2 → task-decomposer agent)
