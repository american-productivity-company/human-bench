# Communications Category

Tests the persona's ability to communicate effectively across different channels. This is the foundational category—if a persona can't communicate, nothing else matters.

## Weight in HLI Score

**10% of total score**

While communication is essential, it's considered a baseline requirement. A persona that communicates perfectly but can't execute complex tasks or remember context isn't particularly useful.

## Subcategories

| Subcategory | Weight | Description |
|-------------|--------|-------------|
| **SMS** | 30% | Text message communication and threading |
| **Email** | 35% | Professional email correspondence |
| **Voice (Inbound)** | 20% | Answering and handling incoming calls |
| **Voice (Outbound)** | 15% | Initiating proactive calls |

## What Belongs Here

### ✅ Include:
- **Channel functionality**: Can the persona send/receive via this channel?
- **Response appropriateness**: Is the tone and format suitable for the medium?
- **Basic conversation flow**: Can it maintain context within a single exchange?
- **Error handling**: Graceful degradation with unclear input

### ❌ Do Not Include:
- **Task execution**: Use the Execution category instead
- **Integration usage**: Use the Integrations category
- **Long-term memory**: Use the Memory category
- **Complex multi-turn conversations**: May belong in Execution (moderate/complex)

## Test Structure

Communication tests focus on the quality and appropriateness of responses:

```yaml
tests:
  - name: Professional email response
    type: email
    from: test_user
    to: test_persona
    subject: "Meeting Request"
    body: "Can we schedule a call next week?"
    benchmark:
      category: communication
      subcategory: email
    expect:
      response_within_seconds: 300
      llm_judge:
        enabled: true
        criteria: |
          The response should:
          - Be professionally formatted
          - Acknowledge the request
          - Provide helpful next steps
        pass_threshold: 0.7
```

## Scoring Criteria

Tests are scored on:
1. **Response speed**: Does it respond within reasonable time?
2. **Appropriateness**: Is the response suitable for the channel and context?
3. **Clarity**: Is the message clear and understandable?
4. **Professionalism**: Does it maintain appropriate tone?

Each test produces a score from 0.0 to 1.0, averaged within each subcategory.

## Contributing New Tests

When adding communication tests:

1. **One channel, one test**: Don't mix SMS and email in a single test
2. **Focus on communication quality**: Not task completion
3. **Use realistic scenarios**: Real messages users would send
4. **Vary complexity**: Include simple greetings, questions, and edge cases

### File Naming Convention

- `{purpose}-{complexity}.yaml` (e.g., `greeting-simple.yaml`, `professional-inquiry.yaml`)
- Group related tests in the same file if they share setup
- Keep test suites under 10 tests for maintainability

## Cross-Category Notes

- **Communication + Execution**: If a test involves both communication AND task completion, it belongs in Execution
- **Communication + Memory**: If testing recall across messages, it belongs in Memory
- **Communication + Integrations**: If using external tools, it belongs in Integrations

Communication tests should be self-contained and focus purely on the quality of the interaction itself.
