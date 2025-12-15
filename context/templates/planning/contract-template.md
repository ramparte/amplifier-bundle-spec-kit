# API Contract: [CONTRACT_NAME]

**Branch**: `[###-feature-name]` | **Date**: [DATE] | **Spec**: [link]  
**Phase**: 1 - Architecture & Data Design  
**Version**: 1.0.0

**Note**: This template is filled in by the plan-architect agent during Phase 1 design. Each API/interface gets its own contract file in `specs/[###-feature]/contracts/`.

---

## Overview

**Purpose**: [What this API/interface provides]

**Consumers**: [Who uses this API - internal modules, external systems, CLI, etc.]

**Provider**: [What module/service implements this API]

**Protocol**: [HTTP REST / gRPC / GraphQL / Python module / CLI / etc.]

**Stability**: [Experimental / Beta / Stable / Deprecated]

---

## Authentication & Authorization

### Authentication

**Method**: [None / API Key / JWT / OAuth 2.0 / mTLS / etc.]

**How to Authenticate**:
```bash
# Example authentication
[authentication example]
```

### Authorization

**Model**: [None / RBAC / ABAC / Token-based / etc.]

**Permissions Required**:
- `[permission1]`: [What it allows]
- `[permission2]`: [What it allows]

---

## Endpoints / Operations

### Operation: [OperationName]

**Purpose**: [What this operation does]

**Stability**: [Stable / Beta / Experimental]

#### HTTP REST Specification

**Method**: `[GET/POST/PUT/PATCH/DELETE]`

**Path**: `/api/v1/[resource]/{id}`

**Path Parameters**:
| Parameter | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| `id` | string | Yes | [Description] | [e.g., UUID format] |

**Query Parameters**:
| Parameter | Type | Required | Description | Default | Constraints |
|-----------|------|----------|-------------|---------|-------------|
| `filter` | string | No | [Description] | null | [e.g., regex pattern] |
| `page` | integer | No | Page number | 1 | [e.g., >= 1] |
| `page_size` | integer | No | Items per page | 20 | [e.g., 1-100] |

**Request Headers**:
| Header | Required | Description | Example |
|--------|----------|-------------|---------|
| `Authorization` | Yes | [Auth method] | `Bearer eyJ0...` |
| `Content-Type` | Yes | Request format | `application/json` |
| `X-Request-ID` | No | Trace ID | `550e8400-e29b-41d4-a716...` |

**Request Body** (if applicable):
```json
{
  "field1": "string",
  "field2": 123,
  "field3": {
    "nested": "object"
  },
  "field4": ["array", "of", "values"]
}
```

**Request Body Schema**:
| Field | Type | Required | Description | Validation |
|-------|------|----------|-------------|------------|
| `field1` | string | Yes | [Purpose] | [e.g., max 255 chars, email format] |
| `field2` | integer | Yes | [Purpose] | [e.g., > 0, <= 1000] |
| `field3` | object | No | [Purpose] | [schema reference] |
| `field4` | array<string> | No | [Purpose] | [e.g., max 10 items] |

**Response Codes**:
| Code | Meaning | When |
|------|---------|------|
| 200 | Success | Operation completed successfully |
| 201 | Created | Resource created successfully |
| 400 | Bad Request | Invalid input |
| 401 | Unauthorized | Missing or invalid authentication |
| 403 | Forbidden | Insufficient permissions |
| 404 | Not Found | Resource doesn't exist |
| 409 | Conflict | Resource already exists or state conflict |
| 422 | Unprocessable Entity | Validation failed |
| 429 | Too Many Requests | Rate limit exceeded |
| 500 | Internal Server Error | Server error |
| 503 | Service Unavailable | Service temporarily unavailable |

**Success Response** (200/201):
```json
{
  "id": "550e8400-e29b-41d4-a716-446655440000",
  "field1": "value",
  "field2": 123,
  "field3": {
    "nested": "value"
  },
  "created_at": "2024-01-15T10:30:00Z",
  "updated_at": "2024-01-15T10:30:00Z"
}
```

**Response Body Schema**:
| Field | Type | Description | Always Present |
|-------|------|-------------|----------------|
| `id` | string | Resource identifier | Yes |
| `field1` | string | [Purpose] | Yes |
| `field2` | integer | [Purpose] | Yes |
| `field3` | object | [Purpose] | No |
| `created_at` | string | ISO 8601 timestamp | Yes |
| `updated_at` | string | ISO 8601 timestamp | Yes |

**Error Response**:
```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable error message",
    "details": {
      "field": ["Validation error message"]
    },
    "request_id": "550e8400-e29b-41d4-a716-446655440000"
  }
}
```

**Error Codes**:
| Code | HTTP Status | Meaning | Recovery Action |
|------|------------|---------|-----------------|
| `INVALID_INPUT` | 400 | [Description] | [How to fix] |
| `RESOURCE_NOT_FOUND` | 404 | [Description] | [How to fix] |
| `DUPLICATE_RESOURCE` | 409 | [Description] | [How to fix] |

#### Examples

**Example 1: Success Case**

Request:
```bash
curl -X POST \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "field1": "example",
    "field2": 42
  }' \
  https://api.example.com/api/v1/resource
```

Response:
```json
{
  "id": "550e8400-e29b-41d4-a716-446655440000",
  "field1": "example",
  "field2": 42,
  "created_at": "2024-01-15T10:30:00Z",
  "updated_at": "2024-01-15T10:30:00Z"
}
```

**Example 2: Validation Error**

Request:
```bash
curl -X POST \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "field1": "",
    "field2": -1
  }' \
  https://api.example.com/api/v1/resource
```

Response (422):
```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input",
    "details": {
      "field1": ["Must not be empty"],
      "field2": ["Must be greater than 0"]
    },
    "request_id": "550e8400-e29b-41d4-a716-446655440000"
  }
}
```

---

### Operation: [NextOperationName]

[Repeat structure above for each operation]

---

## Python Module Contract

**If this is a Python library (per Constitutional Article I)**

### Module: [module_name]

**Import**:
```python
from [package] import [module_name]
```

### Class: [ClassName]

**Purpose**: [What this class provides]

**Constructor**:
```python
def __init__(
    self,
    param1: str,
    param2: int = 10,
    param3: Optional[dict] = None
) -> None:
    """
    Brief description.
    
    Args:
        param1: Description
        param2: Description (default: 10)
        param3: Description (default: None)
        
    Raises:
        ValueError: When [condition]
        TypeError: When [condition]
    """
```

### Method: [method_name]

```python
def method_name(
    self,
    arg1: str,
    arg2: Optional[int] = None
) -> ReturnType:
    """
    Brief description of what method does.
    
    Args:
        arg1: Description of arg1
        arg2: Description of arg2 (optional)
        
    Returns:
        Description of return value
        
    Raises:
        ValueError: When [condition]
        RuntimeError: When [condition]
        
    Examples:
        >>> obj = ClassName(param1="value")
        >>> result = obj.method_name("test")
        >>> print(result)
        expected output
    """
```

**Type Signature**:
```python
def method_name(self, arg1: str, arg2: Optional[int] = None) -> ReturnType: ...
```

**Behavior Contract**:
- **Preconditions**: [What must be true before calling]
- **Postconditions**: [What is guaranteed after calling]
- **Invariants**: [What remains true]

**Example Usage**:
```python
from [package] import [ClassName]

# Create instance
obj = ClassName(param1="value", param2=20)

# Call method
result = obj.method_name("test", arg2=5)

# Use result
print(result.field)
```

---

## CLI Contract

**If this provides CLI (per Constitutional Article II)**

### Command: [command-name]

**Usage**:
```bash
[cli-tool] [command-name] [options] [arguments]
```

**Synopsis**:
```
[command-name] - [brief description]

Usage: [command-name] [--option VALUE] <required-arg>

Description:
    [Detailed description of what command does]
```

**Arguments**:
| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| `<arg1>` | string | Yes | [Description] |
| `<arg2>` | integer | No | [Description] |

**Options**:
| Option | Short | Type | Default | Description |
|--------|-------|------|---------|-------------|
| `--option1` | `-o` | string | null | [Description] |
| `--flag` | `-f` | boolean | false | [Description] |
| `--help` | `-h` | boolean | false | Show help |

**Input**:
- **STDIN**: [What input is read from stdin, if any]
- **Files**: [What files are read, if any]

**Output**:
- **STDOUT**: [What is written to stdout]
- **STDERR**: [What is written to stderr]
- **Files**: [What files are written, if any]

**Exit Codes**:
| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | General error |
| 2 | Invalid usage |
| 3 | [Specific error] |

**Examples**:

**Example 1: Basic usage**
```bash
$ [cli-tool] [command-name] value1
output line 1
output line 2
```

**Example 2: With options**
```bash
$ [cli-tool] [command-name] --option1 value value2
output
```

**Example 3: Piping**
```bash
$ echo "input" | [cli-tool] [command-name]
processed output
```

---

## Data Types

### Type: [TypeName]

**Structure**:
```typescript
interface TypeName {
  field1: string;
  field2: number;
  field3?: OptionalType;  // Optional
  field4: Array<string>;
}
```

**Constraints**:
- `field1`: [Validation rules]
- `field2`: [Validation rules]
- `field3`: [Validation rules]

**JSON Representation**:
```json
{
  "field1": "value",
  "field2": 123,
  "field4": ["item1", "item2"]
}
```

---

## Pagination

**If API supports pagination**

**Query Parameters**:
- `page`: Page number (1-indexed)
- `page_size`: Items per page (default: 20, max: 100)

**Response Format**:
```json
{
  "items": [...],
  "pagination": {
    "page": 1,
    "page_size": 20,
    "total_items": 150,
    "total_pages": 8,
    "has_next": true,
    "has_prev": false
  }
}
```

**Link Header**:
```
Link: <https://api.example.com/resource?page=2>; rel="next",
      <https://api.example.com/resource?page=8>; rel="last"
```

---

## Rate Limiting

**Limits**:
- [e.g., 100 requests per minute per API key]
- [e.g., 1000 requests per hour per IP]

**Headers**:
```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1610712345
```

**Rate Limit Exceeded Response** (429):
```json
{
  "error": {
    "code": "RATE_LIMIT_EXCEEDED",
    "message": "Too many requests. Retry after 60 seconds.",
    "retry_after": 60
  }
}
```

---

## Versioning

**Versioning Strategy**: [URL path / Header / Query parameter]

**Current Version**: `v1`

**Supported Versions**: `v1`

**Deprecated Versions**: None

**Breaking Change Policy**:
- [How breaking changes are communicated]
- [Deprecation timeline - e.g., 6 months notice]
- [Migration guide availability]

---

## Performance Characteristics

**Expected Performance**:
- **Latency**: [e.g., p50: 50ms, p95: 150ms, p99: 500ms]
- **Throughput**: [e.g., 1000 req/s per instance]

**Timeout Recommendations**:
- **Client Timeout**: [e.g., 30 seconds]
- **Retry Strategy**: [e.g., Exponential backoff, max 3 retries]

---

## Idempotency

**Idempotent Operations**:
- `GET`, `PUT`, `DELETE`: Naturally idempotent
- `POST`: [Specify if idempotent and how - e.g., idempotency key]

**Idempotency Key** (if applicable):
```bash
curl -X POST \
  -H "Idempotency-Key: unique-key-123" \
  [...]
```

---

## Testing Contract

### Unit Test Example

```python
def test_operation_success():
    """Test successful operation."""
    # Arrange
    [setup code]
    
    # Act
    result = [operation call]
    
    # Assert
    assert result.[field] == expected_value
    assert [other assertions]
```

### Integration Test Example

```python
def test_operation_integration():
    """Test operation with real dependencies."""
    # Test with real database, external services, etc.
    [integration test code]
```

### Contract Test

```python
def test_response_schema():
    """Verify response matches contract."""
    response = [make request]
    
    # Validate against JSON schema
    validate(response.json(), schema)
```

---

## Security Considerations

**Input Validation**:
- [What validation is performed]
- [How injection attacks are prevented]

**Output Encoding**:
- [How output is encoded to prevent XSS/injection]

**Sensitive Data**:
- [What fields contain sensitive data]
- [How they are protected - encrypted, masked, etc.]

**Access Control**:
- [How authorization is enforced]
- [What principle is followed - e.g., least privilege]

---

## Monitoring & Observability

**Metrics Emitted**:
- `[operation]_requests_total`: Counter of requests
- `[operation]_duration_seconds`: Histogram of request duration
- `[operation]_errors_total`: Counter of errors by type

**Logging**:
- **Info**: Successful operations (with request ID)
- **Warn**: Validation errors, rate limits
- **Error**: Server errors (with stack trace)

**Tracing**:
- Trace ID propagated via `X-Request-ID` header
- Spans created for database queries, external calls

---

## Migration & Deprecation

**Current Contract Version**: 1.0.0

**Deprecation Warnings**: None

**Migration Path** (if contract changes):
- [How to migrate from old contract to new]
- [Backward compatibility window]
- [Tools provided for migration]

---

## Examples for Common Use Cases

### Use Case 1: [Description]

[Step-by-step example showing typical usage]

### Use Case 2: [Description]

[Step-by-step example]

---

## Troubleshooting

### Common Error 1: [Error]

**Symptoms**: [What user sees]

**Cause**: [Why it happens]

**Resolution**: [How to fix]

### Common Error 2: [Error]

[Repeat structure]

---

## Change Log

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | [DATE] | Initial contract |

---

## Contract Approval

**Approved By**: [Name/Role]  
**Approval Date**: [Date]

**Review Schedule**: [e.g., Quarterly, or when breaking changes needed]
