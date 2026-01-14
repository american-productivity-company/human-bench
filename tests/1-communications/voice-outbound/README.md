# Voice Outbound Communication Tests

Tests ability to initiate proactive phone calls.

## Weight: 15% of Communications (1.5% of total HLI)

## What to Test

- Call initiation with clear purpose
- Introduction and permission to speak
- Concise message delivery
- Respecting user's time
- Handling voicemail appropriately
- Follow-up communication

## Test Examples

- Reminder calls
- Notification calls
- Proactive updates
- Callback requests
- Emergency/urgent communications

## File Naming

- `reminder-calls.yaml` - Proactive reminders
- `notification-updates.yaml` - Status updates via call
- `callback-requests.yaml` - Returning user calls
- `voicemail-handling.yaml` - Leaving messages
- `urgent-communications.yaml` - Time-sensitive calls

## Pass Criteria

- Clear statement of purpose within first 10 seconds
- Asks permission to continue ("Is now a good time?")
- Concise delivery (under 2 minutes for most calls)
- Offers alternative communication if user is busy
- Appropriate voicemail messages if no answer
