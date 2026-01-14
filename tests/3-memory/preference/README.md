# Preference Memory Tests

Tests remembering and applying user preferences.

## Weight: 30% of Memory (9% of total HLI)

## ⚠️ Special Penalty
If >50% of preference memory tests fail, a -10 point HLI penalty is applied.

## What to Test
- Communication preferences (call vs text)
- Style preferences (formal vs casual)
- Timing preferences (morning vs evening)
- Multi-party preference tracking
- Preference application without prompting

## Time Requirements
- Minimum delay: 1 hour
- Typical delay: Multiple days
- Should survive intervening conversations

## Test Pattern
1. User mentions preference casually
2. Multiple other interactions (noise)
3. Situation arises where preference applies
4. Verify persona applies preference automatically

## File Naming
- `communication-preference.yaml`
- `style-preference.yaml`
- `timing-preference.yaml`
- `multi-party-preferences.yaml`

## Pass Criteria
- Correct preference applied without reminder
- Appropriate for context
- Distinguishes between different people
- Updates when preferences change
