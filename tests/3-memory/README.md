# Memory & Learning Category

Tests the persona's ability to retain, recall, and apply information over time. Memory is what separates a stateless chatbot from a truly intelligent assistant.

## Weight in HLI Score

**30% of total score**

Memory is the largest non-execution category because it's fundamental to human-like behavior. An assistant that forgets your preferences or can't recall past conversations is frustrating and ineffective.

## Subcategories

| Subcategory | Weight | Description |
|-------------|--------|-------------|
| **Rote Memory** | 30% | Recall specific facts and information |
| **Process Knowledge** | 40% | Learn and replicate multi-step workflows |
| **Preference Memory** | 30% | Remember and apply individual preferences |

### Special Note: Preference Memory Penalty

Preference memory failures are especially problematic because they directly impact user experience. If preference memory tests fail >50%, a **-10 point HLI penalty** is applied to the final score.

## What Belongs Here

### ✅ Include:
- **Information retention**: Can it remember facts shared previously?
- **Workflow learning**: Can it repeat a process after being shown once?
- **Preference application**: Does it remember how different people like to be contacted?
- **Context recall**: Can it reference previous conversations appropriately?

### ❌ Do Not Include:
- **Immediate context**: Information from the current conversation (that's not memory, it's context window)
- **Task execution**: Use Execution category for complex task completion
- **Tool usage**: Use Integrations category for external service calls

## Test Structure

Memory tests require time delays and verification:

```yaml
tests:
  # Phase 1: Teach
  - name: Share dietary preference
    type: text_message
    from: test_user
    to: test_persona
    message: "Just FYI, I'm vegetarian. Please remember that for restaurant recommendations."
    expect:
      response_within_seconds: 300
      llm_judge:
        enabled: true
        criteria: The assistant should acknowledge and confirm it will remember this preference

  # Phase 2: Wait (simulated or real)
  - action: wait
    minutes: 60  # Or longer for realistic testing

  # Phase 3: Verify
  - name: Request recommendation
    type: text_message
    from: test_user
    to: test_persona
    message: "Can you recommend a good restaurant for dinner?"
    benchmark:
      category: memory
      subcategory: preference
    expect:
      response_within_seconds: 300
      llm_judge:
        enabled: true
        criteria: |
          The assistant should:
          - Recommend vegetarian or vegetarian-friendly restaurants
          - Reference the user's dietary preference
          - Not suggest meat-heavy restaurants
        pass_threshold: 0.8
```

## Scoring Criteria

Tests are scored on:
1. **Recall accuracy**: Does it remember the correct information?
2. **Application appropriateness**: Does it use the memory at the right time?
3. **Confidence**: No hallucination or false memories
4. **Persistence**: Memory should survive restarts and time delays

Memory tests typically require higher pass thresholds (0.8+) because incorrect recall can be worse than admitting you don't remember.

## Test Duration Requirements

### Rote Memory
- **Minimum delay**: 30 minutes between teach and recall
- **Typical delay**: 24 hours for realistic testing
- **Content**: Facts, names, dates, preferences, instructions

### Process Knowledge
- **Minimum delay**: 1 hour between demonstration and replication
- **Typical delay**: 1 week to test true retention
- **Content**: Multi-step workflows, procedures, sequences

### Preference Memory
- **Minimum delay**: 1 hour between mention and application
- **Typical delay**: Multiple days with intervening conversations
- **Content**: Communication preferences, style preferences, scheduling preferences

## Contributing New Tests

When adding memory tests:

1. **Include clear teaching phase**: Make it obvious what should be remembered
2. **Appropriate delays**: Don't test "memory" immediately after teaching
3. **Natural recall triggers**: Don't say "Do you remember when I told you X?"
4. **Multiple recall tests**: Test the same memory in different contexts

### File Naming Convention

- `{memory-type}-{content}.yaml` (e.g., `rote-contact-info.yaml`, `preference-communication-style.yaml`)
- `{memory-type}-multi-recall.yaml` for tests with multiple verification points
- Include time delays in test description

## Memory Test Patterns

### Pattern 1: Simple Fact Recall
```yaml
1. User shares fact
2. Wait period
3. User asks question that requires the fact
4. Verify persona uses the fact correctly
```

### Pattern 2: Process Replication
```yaml
1. User demonstrates a multi-step process
2. User explicitly asks persona to remember it
3. Wait period
4. User asks persona to perform the process
5. Verify all steps are executed in correct order
```

### Pattern 3: Preference Application
```yaml
1. User mentions preference casually
2. Multiple other interactions (noise)
3. Situation arises where preference is relevant
4. Verify persona applies preference without prompting
```

### Pattern 4: Multi-Party Preferences
```yaml
1. User A states preference (e.g., "call me")
2. User B states different preference (e.g., "text me")
3. Persona needs to contact both
4. Verify correct method used for each person
```

## Failure Modes to Test

- **False memories**: Persona "remembers" something that was never shared
- **Confusion**: Mixing up information between different people
- **Outdated recall**: Using old information that has been updated
- **Over-application**: Applying preferences in inappropriate contexts
- **Amnesia**: Complete failure to recall recent information

## Cross-Category Considerations

- **Memory + Execution**: Complex tasks that require recalling past procedures belong in Execution (complex/advanced)
- **Memory + Integrations**: If testing memory OF integration data, that may be Integration or Memory depending on focus
- **Memory + Communication**: Memory tests can use any communication channel, but the focus should be on recall, not communication quality

The key question: **Is the test primarily evaluating whether the persona remembered something, or whether it did something well?** If memory is the focus, it belongs here.
