# SMS Communication Tests

Tests text message communication quality, threading, and appropriateness.

## Weight: 30% of Communications (3% of total HLI)

## What to Test

- Response appropriateness for SMS format (concise, clear)
- Handling of abbreviations and informal language
- Threading and context maintenance within conversation
- Response time expectations for async communication
- Error handling with unclear or minimal input

## Test Examples

- Simple greeting and response
- Quick questions (yes/no, simple info)
- Setting reminders via SMS
- Edge cases (empty messages, emoji-only, gibberish)
- Multi-message threading

## File Naming

- `greeting-basic.yaml` - Simple hello/hi tests
- `quick-questions.yaml` - Yes/no and simple info requests
- `reminders-sms.yaml` - Setting reminders via text
- `edge-cases.yaml` - Unusual input handling
- `threading-multi-message.yaml` - Multi-turn conversations

## Pass Criteria

- Response within 5 minutes typical
- Appropriate tone (casual but professional)
- Clear and concise (SMS-appropriate length)
- No formatting issues (no markdown in SMS)
