# Smoke Tests

Quick validation tests to verify core system functionality is operational. These tests are designed to run fast and catch critical failures before running the full benchmark suite.

## Purpose

Smoke tests serve as a sanity check that:
- The testing infrastructure is working correctly
- Personas can be created and respond to basic communication
- No critical regressions have been introduced
- The system is ready for comprehensive benchmarking

## Weight in HLI Score

**Not scored** - Smoke tests are prerequisite checks, not benchmarks. They must pass before HLI scoring begins.

## What Belongs Here

### ✅ Include:
- **Basic health checks**: Can the system create users and personas?
- **Minimal communication tests**: Single SMS and email to verify channels work
- **Quick validation**: Tests that complete in under 5 minutes
- **Binary pass/fail**: Either it works or it doesn't

### ❌ Do Not Include:
- Complex multi-step workflows
- Tests requiring external integrations
- Memory or learning validation
- Performance or quality benchmarks

## Test Structure

Smoke tests should be minimal and fast:

```yaml
version: "1.0"
name: Smoke Tests
description: Quick validation tests
environment: dev
timeout_seconds: 300

tests:
  - name: SMS Smoke Test
    type: text_message
    from: test_user
    to: test_persona
    message: "Are you there?"
    expect:
      response_within_seconds: 120
      llm_judge:
        enabled: true
        criteria: Any coherent response is acceptable
        pass_threshold: 0.5  # Very lenient
```

## Scoring Criteria

**Pass**: System responds within timeout with any coherent message
**Fail**: No response, error, or completely nonsensical output

Smoke tests use lenient LLM judge thresholds (0.5) because we only care about basic functionality, not quality.

## Contributing New Tests

Before adding a smoke test, ask:
1. **Is this a critical failure detector?** If the system can't do this, nothing else matters.
2. **Can it run in under 2 minutes?** Smoke tests must be fast.
3. **Is it truly minimal?** One message, one response, done.

If you answered yes to all three, add your test here. Otherwise, it belongs in a benchmark category.

### File Naming Convention

- `basic-health.yaml` - Core system functionality
- `{channel}-smoke.yaml` - Single channel validation (e.g., `sms-smoke.yaml`)

Keep it simple. Smoke tests are the canary in the coal mine—they should fail fast and fail loud when something is fundamentally broken.
