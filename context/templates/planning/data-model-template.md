# Data Model: [FEATURE]

**Branch**: `[###-feature-name]` | **Date**: [DATE] | **Spec**: [link]  
**Phase**: 1 - Architecture & Data Design  
**Input**: Specification + Research findings

**Note**: This template is filled in by the plan-architect agent during Phase 1 design.

---

## Overview

**Purpose**: [What data this model represents and why it exists]

**Scope**: [What's included in this data model vs what's external]

**Key Entities from Spec**:
- [Entity1] - [Brief description from spec]
- [Entity2] - [Brief description from spec]
- [Entity3] - [Brief description from spec]

---

## Entity Definitions

### Entity: [EntityName]

**Description**: [What this entity represents]

**Lifecycle**: [Created when... Updated when... Deleted when...]

**Access Patterns**:
- [How this entity is primarily queried]
- [Common filter/search requirements]
- [Expected read/write ratio]

#### Attributes

| Attribute | Type | Required | Description | Validation Rules |
|-----------|------|----------|-------------|------------------|
| `id` | UUID/Integer | Yes | Unique identifier | Auto-generated |
| `[attribute1]` | [type] | Yes/No | [Purpose] | [e.g., max 255 chars, must be email] |
| `[attribute2]` | [type] | Yes/No | [Purpose] | [e.g., >0, enum: [A,B,C]] |
| `created_at` | DateTime | Yes | Creation timestamp | Auto-set on create |
| `updated_at` | DateTime | Yes | Last update timestamp | Auto-update on modify |

#### Relationships

| Related Entity | Type | Description | Cascade Behavior |
|----------------|------|-------------|------------------|
| [Entity2] | One-to-Many | [Explanation] | Delete: [CASCADE/SET NULL/RESTRICT] |
| [Entity3] | Many-to-Many | [Explanation] | Delete: [Strategy] |

#### Invariants

[Business rules that must always be true for this entity]

- [Invariant 1: e.g., "status can only transition from draft → published → archived"]
- [Invariant 2: e.g., "end_date must be after start_date"]
- [Invariant 3: e.g., "user_id must reference an active user"]

#### Indexes

[Indexes required for performance based on access patterns]

- **Primary**: `id`
- **Unique**: `[field_name]` - [Reason for uniqueness]
- **Index**: `[field_name]` - [Query pattern this supports]
- **Composite**: `([field1], [field2])` - [Query pattern this supports]

---

### Entity: [NextEntityName]

[Repeat structure above for each entity]

---

## Entity Relationship Diagram

```
┌─────────────────┐
│   Entity1       │
│─────────────────│
│ id (PK)         │
│ attribute1      │◄──────┐
│ attribute2      │       │
│ created_at      │       │ One-to-Many
│ updated_at      │       │
└─────────────────┘       │
                          │
                          │
┌─────────────────┐       │
│   Entity2       │       │
│─────────────────│       │
│ id (PK)         │───────┘
│ entity1_id (FK) │
│ attribute_x     │
│ attribute_y     │
└─────────────────┘
```

[Create ASCII diagram showing relationships between entities]

---

## Storage Strategy

### Persistence Layer

**Storage Type**: [SQL Database / NoSQL / File System / Hybrid]

**Rationale**: [Why this storage type based on research and requirements]

**Schema Management**:
- **Migrations**: [Strategy - e.g., Alembic, Django migrations, manual SQL]
- **Versioning**: [How schema versions are tracked]
- **Backward Compatibility**: [How schema changes are handled in production]

### Data Access Patterns

#### Primary Access Patterns

1. **Pattern**: [e.g., "Retrieve user with all orders"]
   - **Frequency**: [High / Medium / Low]
   - **Query**: [Pseudo-query or description]
   - **Optimization**: [Index or caching strategy]

2. **Pattern**: [e.g., "Search products by category and price range"]
   - **Frequency**: [High / Medium / Low]
   - **Query**: [Pseudo-query or description]
   - **Optimization**: [Index or caching strategy]

#### Write Patterns

1. **Pattern**: [e.g., "Create order with line items (transaction)"]
   - **Frequency**: [High / Medium / Low]
   - **Constraints**: [Transactional requirements, locking needs]

---

## Data Validation

### Entity-Level Validation

[Validation rules that apply to individual entities]

**[EntityName]**:
- **Required Fields**: [List]
- **Format Validation**: [Rules for string formats, patterns]
- **Range Validation**: [Rules for numeric bounds]
- **Business Logic**: [Complex validation rules]

### Cross-Entity Validation

[Validation rules that span multiple entities]

- [Rule 1: e.g., "Total order amount must match sum of line item amounts"]
- [Rule 2: e.g., "User cannot have overlapping reservations"]

### Enforcement Strategy

- **Application Layer**: [What validation happens in code]
- **Database Layer**: [What constraints are in the database]
- **Rationale**: [Why this division of responsibilities]

---

## State Management

### Entity States

**[EntityName] States**:

```
┌─────────┐     ┌───────────┐     ┌──────────┐
│  draft  │────►│ published │────►│ archived │
└─────────┘     └───────────┘     └──────────┘
    ▲                                   │
    └───────────────────────────────────┘
              (can reopen)
```

**Valid Transitions**:
- `draft → published`: [Conditions required]
- `published → archived`: [Conditions required]
- `archived → draft`: [Conditions required]

**Invalid Transitions**:
- `draft → archived`: [Why this is blocked]

### Audit Trail

**Requirement**: [Yes / No / Partial]

**Implementation**:
- [Approach: e.g., separate audit table, event sourcing, append-only log]
- [What is tracked: who, when, what changed]
- [Retention policy]

---

## Data Integrity

### Referential Integrity

**Foreign Key Constraints**:
- [Entity.field → ReferencedEntity.field] - [CASCADE/RESTRICT/SET NULL]

**Orphan Prevention**:
- [Strategy to prevent orphaned records]

### Consistency Requirements

**Eventual Consistency**: [Acceptable / Not Acceptable]

**Strong Consistency Required For**:
- [List operations that require strong consistency]

**Consistency Boundaries**:
- [What data must be consistent within a transaction]

---

## Performance Considerations

### Query Performance

**Expected Load**:
- **Read QPS**: [Queries per second estimate]
- **Write QPS**: [Queries per second estimate]
- **Peak Load Multiplier**: [e.g., 3x during business hours]

**Optimization Strategies**:
- [Caching approach if needed]
- [Index strategy]
- [Query optimization notes]

### Scaling Strategy

**Vertical Scaling Limit**: [When vertical scaling becomes insufficient]

**Horizontal Scaling**:
- **Sharding Strategy**: [If applicable - how data is partitioned]
- **Replication**: [Read replicas strategy]

---

## Security & Privacy

### Sensitive Data

**PII (Personally Identifiable Information)**:
- [List fields containing PII]
- [Storage strategy: encrypted at rest / hashed / tokenized]

**Access Control**:
- [Who can read this data]
- [Who can modify this data]
- [How access is enforced]

### Compliance Requirements

[Any regulatory requirements affecting data model]

- **GDPR**: [Right to deletion, data portability considerations]
- **HIPAA**: [Health data protection requirements]
- **PCI-DSS**: [Payment card data requirements]
- **Other**: [Jurisdiction-specific requirements]

---

## Migration Strategy

### From Existing System (if applicable)

**Source System**: [Description]

**Migration Approach**: [Big bang / Phased / Parallel run]

**Data Transformation**:
- [Mapping from old schema to new schema]
- [Data cleanup required]

**Rollback Strategy**: [How to revert if migration fails]

### Schema Evolution

**Versioning Strategy**: [How schema versions are managed]

**Backward Compatibility**: [Requirements for schema changes]

**Forward Compatibility**: [Can old code work with new schema]

---

## Testing Strategy

### Unit Tests

**Entity Validation Tests**:
- [Test valid entity creation]
- [Test validation rules enforcement]
- [Test state transitions]

### Integration Tests

**Database Integration**:
- [Test CRUD operations]
- [Test transactions]
- [Test constraints]
- [Test indexes work as expected]

### Data Quality Tests

**Invariant Tests**:
- [Verify business rules hold across operations]
- [Test referential integrity]
- [Test data consistency]

---

## Documentation Requirements

### For Developers

- **Schema Documentation**: [Where schema is documented - e.g., in-code comments, separate docs]
- **ER Diagrams**: [This document + any auto-generated diagrams]
- **Access Patterns**: [Query examples, common operations]

### For Operations

- **Backup Strategy**: [What needs to be backed up, frequency]
- **Restore Procedures**: [How to restore from backup]
- **Monitoring**: [What database metrics to monitor]

---

## Open Questions

[Any unresolved questions about the data model]

- [ ] [Question 1]
- [ ] [Question 2]

---

## Constitutional Compliance

### Library-First Principle

**Compliance**: [How this data model supports library-first approach]

[Entities should be framework-agnostic where possible]

### Test-First Development

**Test Data Strategy**:
- [How test data will be created]
- [Fixtures vs factories]
- [Test database strategy]

---

## Approval

**Data Model Approved By**: [Name] on [Date]

**Changes Since Approval**: [Log of changes after approval]

---

## Appendix: Sample Data

### Sample Entity1

```json
{
  "id": "550e8400-e29b-41d4-a716-446655440000",
  "attribute1": "example value",
  "attribute2": 42,
  "created_at": "2024-01-15T10:30:00Z",
  "updated_at": "2024-01-15T10:30:00Z"
}
```

[Include sample data for each entity showing typical values]
