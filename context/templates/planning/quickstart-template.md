# Quickstart Guide: [FEATURE]

**Branch**: `[###-feature-name]` | **Date**: [DATE] | **Spec**: [link]  
**Phase**: 1 - Architecture & Data Design  
**Purpose**: Validate the feature with end-to-end scenarios before full implementation

**Note**: This template is filled in by the plan-architect agent during Phase 1 design. It defines minimal validation scenarios that prove the feature works end-to-end.

---

## Purpose

This quickstart guide defines the **minimal set of scenarios** needed to validate that the [FEATURE] feature works end-to-end. These scenarios are derived from the Priority 1 (P1) user stories in the specification and serve as acceptance criteria for implementation.

**Use Cases**:
1. **Pre-Implementation**: Understand what "done" looks like
2. **During Implementation**: Validate each milestone
3. **Post-Implementation**: Smoke test the complete feature
4. **Documentation**: Foundation for user documentation

---

## Prerequisites

### Environment Setup

**Required**:
- [Runtime: e.g., Python 3.11+, Node.js 20+]
- [Dependencies: e.g., PostgreSQL 15, Redis 7]
- [Tools: e.g., curl, jq, or specific CLI]

**Installation**:
```bash
# Clone repository
git clone [repo-url]
cd [repo-name]

# Install dependencies
[package-manager install command]

# Configure environment
cp .env.example .env
# Edit .env with required values

# Initialize database (if applicable)
[migration/setup command]
```

### Test Data

[What test data is needed to run scenarios]

**Option 1: Use provided fixtures**
```bash
[command to load test data]
```

**Option 2: Create manually**
```bash
[commands to create minimal test data]
```

---

## Scenario 1: [P1 User Story Title]

**User Story Reference**: [US-001 from specification]

**Goal**: [What this scenario validates]

**Estimated Time**: [e.g., 2 minutes]

### Setup

```bash
# Any setup specific to this scenario
[commands if needed]
```

### Steps

**Step 1: [Action]**

```bash
# Command
[exact command to run]
```

**Expected Output**:
```
[expected output]
```

**What to verify**:
- [ ] [Specific thing to check]
- [ ] [Another thing to check]

---

**Step 2: [Next Action]**

```bash
# Command
[exact command to run]
```

**Expected Output**:
```
[expected output]
```

**What to verify**:
- [ ] [Specific thing to check]
- [ ] [Another thing to check]

---

**Step 3: [Final Action]**

```bash
# Command
[exact command to run]
```

**Expected Output**:
```
[expected output]
```

**What to verify**:
- [ ] [Specific thing to check]
- [ ] [Another thing to check]

### Success Criteria

✅ **Scenario passes if**:
- [Criterion 1 from specification]
- [Criterion 2 from specification]
- [Criterion 3 from specification]

❌ **Common Failure Points**:
- [Known issue 1 and how to diagnose]
- [Known issue 2 and how to diagnose]

### Cleanup

```bash
# Commands to clean up after scenario
[cleanup commands if needed]
```

---

## Scenario 2: [Next P1 User Story]

[Repeat structure above for each P1 user story]

---

## Scenario 3: [Integration Scenario]

**Goal**: Validate that multiple features work together

**User Story References**: [US-001, US-002, US-003]

[Follow same structure as Scenario 1]

---

## Edge Case Validation

### Edge Case 1: [Description]

**What it tests**: [Edge case from specification]

**How to trigger**:
```bash
[command or sequence that triggers edge case]
```

**Expected behavior**: [What should happen]

**Validation**:
- [ ] [Check 1]
- [ ] [Check 2]

### Edge Case 2: [Description]

[Repeat structure]

---

## Error Handling Validation

### Error 1: [Error Condition]

**Trigger**:
```bash
[command that triggers error]
```

**Expected Error**:
```
[error message format]
```

**Validation**:
- [ ] Error message is clear and actionable
- [ ] System remains in consistent state
- [ ] Appropriate HTTP status code (if API)

### Error 2: [Error Condition]

[Repeat structure]

---

## Performance Validation (Optional)

**If performance is a success criterion from specification**

### Load Test

**Scenario**: [What to test]

**Load Pattern**:
- [e.g., 100 requests/second for 60 seconds]
- [e.g., 10 concurrent users for 5 minutes]

**Commands**:
```bash
# Using appropriate load testing tool
[load test command]
```

**Success Criteria**:
- [ ] [Metric 1: e.g., p95 latency < 100ms]
- [ ] [Metric 2: e.g., error rate < 1%]
- [ ] [Metric 3: e.g., throughput > 500 req/s]

---

## Security Validation (Optional)

**If security is a success criterion from specification**

### Authentication Test

**Scenario**: Verify authentication is enforced

**Test 1: Access without authentication**
```bash
[command without auth credentials]
```
**Expected**: [401 Unauthorized or appropriate error]

**Test 2: Access with invalid credentials**
```bash
[command with invalid credentials]
```
**Expected**: [401/403 error]

**Test 3: Access with valid credentials**
```bash
[command with valid credentials]
```
**Expected**: [Success response]

### Authorization Test

[Test that users can only access what they're authorized for]

---

## CLI Usage Examples

**If feature includes CLI per Constitutional Article II**

### Basic Usage

**Help output**:
```bash
[cli-command] --help
```

**Expected**:
```
[help text showing available commands and options]
```

### Common Commands

**Command 1: [Most common operation]**
```bash
[command with typical options]
```

**Command 2: [Second most common operation]**
```bash
[command with typical options]
```

### Piping and Composition

**Example: Chaining commands**
```bash
[command1] | [command2] | [command3]
```

**Output**:
```
[expected output]
```

---

## Integration Points

### Integration 1: [External System/API]

**What it validates**: [Integration from specification]

**Setup**:
```bash
# Configure integration
[configuration commands]
```

**Test**:
```bash
# Trigger integration
[test command]
```

**Verify**:
- [ ] [External system receives expected data]
- [ ] [Response is handled correctly]
- [ ] [Error cases are handled gracefully]

### Integration 2: [Another Integration]

[Repeat structure]

---

## Observability Check

**Per Constitutional Article VII**

### Logging

**Verify logs are produced**:
```bash
# Trigger operation
[command]

# Check logs
[log viewing command]
```

**Expected log entries**:
- [ ] Info: [Expected info log]
- [ ] Error: [Expected error log if error triggered]
- [ ] Audit: [Expected audit log if applicable]

### Metrics (if applicable)

**Verify metrics are emitted**:
```bash
# View metrics endpoint
[metrics command]
```

**Expected metrics**:
- [ ] [Counter: operation_total]
- [ ] [Histogram: operation_duration]
- [ ] [Gauge: current_connections (if applicable)]

---

## Rollback Validation

**Verify feature can be safely disabled**

### Rollback Scenario

**Step 1: Disable feature**
```bash
[command or config change to disable]
```

**Step 2: Verify system still functions**
```bash
# Test that unrelated features still work
[validation commands]
```

**Step 3: Verify graceful degradation**
```bash
# Test that feature returns appropriate "not available" response
[test command]
```

---

## Automated Test Equivalents

**Map quickstart scenarios to automated tests**

| Scenario | Test Location | Test Name |
|----------|--------------|-----------|
| Scenario 1 | [path/to/test/file.py] | test_[scenario_name] |
| Scenario 2 | [path/to/test/file.py] | test_[scenario_name] |
| Edge Case 1 | [path/to/test/file.py] | test_[edge_case_name] |

**Running automated tests**:
```bash
[test command to run all related tests]
```

---

## Troubleshooting

### Issue 1: [Common Problem]

**Symptoms**: [What user sees]

**Diagnosis**:
```bash
# Commands to diagnose
[diagnostic commands]
```

**Resolution**: [How to fix]

### Issue 2: [Another Common Problem]

[Repeat structure]

---

## Success Checklist

Use this checklist to verify feature is ready:

**Functionality**:
- [ ] All P1 scenarios pass
- [ ] Edge cases handled correctly
- [ ] Error messages are clear

**Performance**:
- [ ] Meets performance success criteria from specification
- [ ] No obvious performance regressions

**Security**:
- [ ] Authentication enforced
- [ ] Authorization rules work correctly
- [ ] No sensitive data leaked in errors

**Constitutional Compliance**:
- [ ] Library usable programmatically
- [ ] CLI provided with text I/O
- [ ] Observable (logs/metrics present)

**Documentation**:
- [ ] All commands documented
- [ ] Examples are runnable
- [ ] Common issues addressed

---

## Next Steps

**After Quickstart Validation Passes**:

1. **Expand Documentation**
   - Add detailed user guide
   - Create API reference
   - Document configuration options

2. **Expand Test Coverage**
   - Add unit tests for internal logic
   - Add integration tests for complex scenarios
   - Add performance regression tests

3. **Production Readiness**
   - Add monitoring and alerting
   - Create runbooks for operations
   - Plan deployment strategy

---

## Feedback

**As you use this quickstart guide, note**:
- [ ] Steps that were confusing
- [ ] Missing prerequisites
- [ ] Incorrect expected outputs
- [ ] Additional scenarios needed

[Location to report feedback - e.g., GitHub issues]
