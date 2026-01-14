# Integrations Category

Tests the persona's ability to interact with external services and tools. A persona is only as useful as the systems it can access.

## Weight in HLI Score

**20% of total score**

Integrations are critical for real-world utility. A persona that can't check your calendar, send emails, or update your CRM is severely limited.

## Subcategories

| Subcategory | Weight | Description |
|-------------|--------|-------------|
| **Email Services** | 20% | Gmail, Outlook integration (read/send/organize) |
| **Calendar** | 20% | Google Calendar, Outlook Calendar (events, scheduling) |
| **CRM** | 20% | Salesforce, HubSpot, Pipedrive (contacts, deals) |
| **Project Management** | 20% | Asana, Notion, Linear, Jira (tasks, projects) |
| **Financial** | 20% | Stripe, QuickBooks (payments, invoices) |

## What Belongs Here

### ✅ Include:
- **Service authentication**: Can it connect and authenticate?
- **Basic operations**: Read, create, update, delete actions
- **Data accuracy**: Does it fetch/modify the correct information?
- **Error handling**: Graceful failures with permission issues or API errors

### ❌ Do Not Include:
- **Communication quality**: Use Communications category
- **Complex workflows**: If it involves multiple integrations and decision-making, use Execution (complex/advanced)
- **Memory of past integrations**: Use Memory category

## Test Structure

Integration tests validate correct tool usage:

```yaml
tests:
  - name: Create calendar event
    type: integration
    integration: calendar
    action: create_event
    from: test_user
    to: test_persona
    message: "Please schedule a team meeting for next Tuesday at 2pm"
    benchmark:
      category: integrations
      subcategory: calendar
    expect:
      response_within_seconds: 600
      integration_used: google_calendar
      action_completed: true
      llm_judge:
        enabled: true
        criteria: |
          The persona should:
          - Successfully create a calendar event
          - Confirm the event details (date, time)
          - Provide meeting link or location if applicable
        pass_threshold: 0.8
```

## Scoring Criteria

Tests are scored on:
1. **Correct tool selection**: Did it use the right integration?
2. **Action completion**: Was the operation successful?
3. **Data accuracy**: Are the parameters correct (dates, amounts, names)?
4. **Confirmation quality**: Does it clearly communicate what happened?

Integration tests typically have higher pass thresholds (0.8+) because incorrect tool usage can have real consequences.

## Test Requirements

### Prerequisites

Tests in this category require:
- **Authenticated connections**: Personas must have connections configured
- **Test accounts**: Sandbox/test accounts for each service
- **Webhooks**: Some integrations require webhook verification

### Test Data

- Use isolated test data (test calendars, demo CRM accounts)
- Clean up created resources in teardown
- Never use production systems

## Contributing New Tests

When adding integration tests:

1. **One integration per test**: Don't test calendar + CRM in the same test
2. **Test happy path first**: Basic CRUD operations before edge cases
3. **Include error scenarios**: Permission denied, rate limits, invalid data
4. **Verify side effects**: Check that the action actually happened in the external system

### File Naming Convention

- `{service}-{action}.yaml` (e.g., `gmail-send-email.yaml`, `salesforce-create-contact.yaml`)
- `{service}-error-handling.yaml` for error scenarios
- Group related operations in the same file if they share setup

## Supported Integrations

Current integrations available for testing:

### Email Services
- Gmail (via Composio)
- Outlook (via Composio)

### Calendar
- Google Calendar (via Composio)
- Outlook Calendar (via Composio)

### CRM
- Salesforce (via Composio)
- HubSpot (via Composio)
- Pipedrive (via Composio)

### Project Management
- Asana (via Composio)
- Notion (via Composio)
- Linear (via Composio)
- Jira (via Composio)

### Financial
- Stripe (via Composio)
- QuickBooks (via Composio)

## Integration vs. Execution

**Rule of thumb**: If the test is primarily about using a tool correctly, it's an Integration test. If it's about orchestrating multiple tools or making complex decisions, it's an Execution test.

Examples:
- ✅ Integration: "Send an email via Gmail" 
- ❌ Integration: "Research competitors and email me a summary" (this is Execution: complex)
- ✅ Integration: "Create a contact in Salesforce"
- ❌ Integration: "Update all contacts from last month's leads" (this is Execution: moderate/complex)
