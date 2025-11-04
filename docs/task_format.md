# Human-Bench Task Format Specification

This document defines the YAML format for Human-Bench tasks.

## Basic Structure

```yaml
task_id: "SMS-001"              # Unique identifier (required)
level: 1                        # Difficulty level 1-8 (required)
category: "string"              # Task category (required)
channel: "SMS"                  # Primary channel (required)
channels: ["SMS", "Email"]      # For multi-channel tasks (optional)
difficulty: "easy"              # easy|medium|hard|very_hard|extreme (required)

description: |                  # What this task tests (required)
  Human-readable description

input:                          # Task input (required)
  from: "+15551234567"
  to: "{{persona_phone}}"
  content: "Message content"
  timestamp: "2025-01-15T14:00:00-08:00"

success_criteria:              # Evaluation criteria (required)
  - type: "response_time"
    max_seconds: 30
    weight: 0.2               # Must sum to 1.0

metadata:                      # Task metadata (required)
  estimated_duration: "10s"
  requires_external_tools: ["web_search"]
  tags: ["tag1", "tag2"]
```

See task files in `tasks/` for complete examples.
