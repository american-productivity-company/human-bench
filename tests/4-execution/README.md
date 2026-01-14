# Execution Category

Tests the persona's ability to complete tasks of varying complexity. This is the largest category because task completion is the primary value proposition of an AI assistant.

## Weight in HLI Score

**40% of total score**

Execution is the heaviest-weighted category because it represents real-world utility. A persona that communicates beautifully but can't get things done isn't useful.

## Subcategories

| Subcategory | Weight | Multiplier | Description |
|-------------|--------|------------|-------------|
| **Simple** | 10% | 1.0x | Single-step, unambiguous tasks |
| **Moderate** | 25% | 1.2x | Multi-step tasks with clear paths |
| **Complex** | 35% | 1.5x | Tasks requiring judgment and synthesis |
| **Advanced** | 30% | 2.0x | Extended tasks with adaptation and recovery |

### Complexity Multipliers

While weights determine the subcategory importance, multipliers can be applied in advanced scoring algorithms to emphasize difficulty. A persona that excels at advanced tasks should be rewarded more than one that only handles simple tasks.

## What Belongs Here

### ✅ Include:
- **Task completion**: Did the persona accomplish the goal?
- **Multi-step orchestration**: Can it coordinate multiple actions?
- **Decision-making**: Does it make appropriate choices when options exist?
- **Error recovery**: Can it adapt when things don't go as planned?
- **Judgment calls**: Can it prioritize and determine appropriate action?

### ❌ Do Not Include:
- **Pure communication**: Use Communications category
- **Simple tool usage**: Use Integrations category
- **Memory recall**: Use Memory category (unless the task is complex AND requires memory)

## Complexity Level Definitions

### Simple (10% weight, 1.0x multiplier)

**Characteristics:**
- Single-step operation
- Clear, unambiguous instructions
- One correct answer
- Minimal context required
- Immediate execution

**Examples:**
- "Remind me to call Mom at 5pm"
- "What's on my calendar tomorrow?"
- "Send an email to john@example.com saying I'll be late"

**Test Structure:**
```yaml
- name: Set simple reminder
  type: text_message
  from: test_user
  to: test_persona
  message: "Remind me to call Mom at 5pm today"
  benchmark:
    category: execution
    subcategory: simple
    complexity_level: simple
  expect:
    response_within_seconds: 300
    llm_judge:
      enabled: true
      criteria: |
        The assistant should:
        - Confirm the reminder is set
        - Repeat back the time and action
      pass_threshold: 0.7
```

### Moderate (25% weight, 1.2x multiplier)

**Characteristics:**
- 2-4 sequential steps
- Some decision-making required
- Clear success criteria
- May involve coordination
- Single domain/context

**Examples:**
- "Schedule a meeting with the team and send the agenda"
- "Book a restaurant and send me directions"
- "Find the Q3 report and summarize key metrics"

**Test Structure:**
```yaml
- name: Schedule meeting with agenda
  type: text_message
  from: test_user
  to: test_persona
  message: "Schedule a 1-hour team meeting next Tuesday and send everyone an agenda covering Q1 goals, Q2 planning, and budget review"
  benchmark:
    category: execution
    subcategory: moderate
    complexity_level: moderate
  expect:
    response_within_seconds: 600
    llm_judge:
      enabled: true
      criteria: |
        The assistant should:
        - Check calendars for availability
        - Create the meeting event
        - Generate a structured agenda with the three topics
        - Send the agenda to attendees
      pass_threshold: 0.75
```

### Complex (35% weight, 1.5x multiplier)

**Characteristics:**
- 5+ steps with dependencies
- Requires judgment and prioritization
- Multiple valid approaches
- Cross-domain coordination
- Synthesis of information
- Ambiguity resolution

**Examples:**
- "Research our competitors and prepare a summary report"
- "Coordinate schedules between London and NY teams for a project kickoff"
- "Help me prepare for next week's board meeting"

**Test Structure:**
```yaml
- name: Competitor research and analysis
  type: email
  from: test_user
  to: test_persona
  subject: "Competitor Analysis Request"
  body: |
    I need to understand our competitive landscape before the strategy meeting.
    Can you research our top 3 competitors and summarize:
    - Their recent product launches
    - Pricing strategy
    - Market positioning
    
    Please have this ready by end of week.
  benchmark:
    category: execution
    subcategory: complex
    complexity_level: complex
  expect:
    response_within_seconds: 1800  # 30 minutes
    llm_judge:
      enabled: true
      criteria: |
        The assistant should:
        - Acknowledge the request and timeline
        - Clarify which competitors if ambiguous
        - Outline their research approach
        - Provide a structured summary document
        - Include credible sources
      pass_threshold: 0.8
```

### Advanced (30% weight, 2.0x multiplier)

**Characteristics:**
- Extended multi-day tasks
- Significant ambiguity
- Proactive problem-solving
- Error detection and recovery
- Adaptive strategy
- Multiple stakeholder coordination

**Examples:**
- "Manage client onboarding across sales, legal, and success teams"
- "Plan and coordinate our quarterly offsite including logistics, agenda, and follow-ups"
- "Help me launch our new product, handling announcements, docs, and customer migration"

**Test Structure:**
```yaml
- name: Plan company offsite
  type: email
  from: test_user
  to: test_persona
  subject: "Need Help Planning Q2 Offsite"
  body: |
    We need to plan our Q2 offsite for 30 people. 
    Budget is $50k. Should be within 2 hours of SF.
    Need venue, agenda, team building activities, and catering.
    Event is in 6 weeks.
  benchmark:
    category: execution
    subcategory: advanced
    complexity_level: advanced
  expect:
    response_within_seconds: 3600  # 1 hour for initial response
    llm_judge:
      enabled: true
      criteria: |
        The assistant should:
        - Break down into clear workstreams (venue, agenda, activities, logistics)
        - Ask clarifying questions about priorities
        - Propose a timeline with milestones
        - Identify dependencies (venue before catering, etc.)
        - Suggest specific options with pros/cons
        - Proactively flag potential issues (budget, timing, capacity)
        - Offer to manage the execution
      pass_threshold: 0.85
```

## Scoring Criteria

Tests are scored on:
1. **Completion**: Was the task accomplished?
2. **Efficiency**: Appropriate number of steps (not over or under-engineered)?
3. **Quality**: Is the output accurate and useful?
4. **Communication**: Clear updates and confirmation?
5. **Error handling**: Graceful recovery from issues?
6. **Judgment**: Good decisions when choices were required?

## Test Duration Guidelines

| Complexity | Expected Duration | Timeout |
|------------|------------------|---------|
| Simple | < 5 minutes | 10 minutes |
| Moderate | 5-15 minutes | 30 minutes |
| Complex | 15-60 minutes | 2 hours |
| Advanced | Hours to days | Varies by task |

## Contributing New Tests

When adding execution tests:

1. **Classify correctly**: Be honest about complexity
2. **Clear success criteria**: What does "done" look like?
3. **Realistic scenarios**: Based on real user needs
4. **Test at boundaries**: Include tasks that might fail
5. **Document expected behavior**: Especially for complex/advanced

### File Naming Convention

- `{domain}-{complexity}.yaml` (e.g., `scheduling-moderate.yaml`, `research-complex.yaml`)
- `{scenario}-end-to-end.yaml` for comprehensive workflows
- Keep test suites focused on one complexity level

## Complexity Decision Tree

Use this to determine the right subcategory:

```
Is it a single, clear action?
├─ YES → Simple
└─ NO ↓

Does it require 2-4 sequential steps with minimal judgment?
├─ YES → Moderate
└─ NO ↓

Does it involve synthesis, research, or cross-domain coordination?
├─ YES → Complex
└─ NO ↓

Does it require extended time, adaptive strategy, or multi-stakeholder coordination?
├─ YES → Advanced
└─ UNSURE → Probably Complex or Advanced
```

## Examples by Complexity

### Simple
- Set a reminder
- Send a message
- Look up information
- Create a calendar event
- Make a single API call

### Moderate
- Schedule a meeting and send agenda
- Book travel and send confirmation
- Update CRM records after a call
- Generate and send a report
- Coordinate a single deliverable

### Complex
- Research and synthesize information
- Plan a multi-step project
- Coordinate across multiple systems
- Resolve scheduling conflicts
- Prepare comprehensive materials

### Advanced
- Manage extended projects (weeks)
- Handle client onboarding end-to-end
- Coordinate cross-functional initiatives
- Adapt strategy based on changing requirements
- Proactively identify and solve problems

## Cross-Category Considerations

Many tests will span multiple categories. Here's how to decide:

**Execution + Memory**: If the task is complex AND requires recall, it's Execution (the complexity is the focus)

**Execution + Integrations**: If using a tool is the main challenge, it's Integrations. If orchestrating multiple tools toward a goal, it's Execution

**Execution + Communication**: If the task is primarily about communication quality, it's Communication. If it's about accomplishing something VIA communication, it's Execution

**Rule of thumb**: If the primary evaluation criterion is "Did it accomplish the goal?" → Execution category
