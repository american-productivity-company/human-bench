# Human-Bench 🤖→🧑

**A benchmark for human-like capability from virtual humans made of AI Agents.**

Human-Bench evaluates AI agents on realistic, multi-modal communication tasks that mirror how humans actually interact with personal assistants—across SMS, email, and voice calls, with context that spans days or weeks.

## Why Human-Bench?

Existing benchmarks test coding ability (SWE-bench), general reasoning (GAIA), or tool use (τ-bench). But none evaluate what makes a truly useful personal assistant:

- 📱 **Multi-modal communication** (SMS, Email, Voice)
- 🔗 **Cross-channel context** ("About that email I sent..." during a phone call)
- ⚡ **Priority management** (handling interruptions gracefully)
- 📅 **Long-term coherence** (planning a wedding over weeks)
- 🎯 **Human-like interaction patterns** (not just Q&A)

## How It Works

**Human-Bench is a hosted benchmark service.** We handle all testing and evaluation.

1. **Register your AI assistant** at [humanbench.ai](https://humanbench.ai)
2. **Provide contact info**: Your persona's phone number, email, and name
3. **We run the tests**: We send SMS, emails, and phone calls to your assistant
4. **Get your score**: See detailed results and compare on the public leaderboard

No setup required - just register and test!

## Benchmark Structure

```
Level 1: Basic (Single turn, single channel)         → Target: 95%+ success
Level 2: Multi-Turn (Conversations)                  → Target: 85%+ success
Level 3: Cross-Modal (Context across channels)       → Target: 70%+ success
Level 4: Priority Management (Interruptions)         → Target: 60%+ success
Level 5: Long-Term Projects (Days/weeks)             → Target: 40%+ success
```

**Total: 300 tasks** across 5 difficulty levels, testing real-world personal assistant capabilities.

**🔗 Test Your Assistant**: [humanbench.ai](https://humanbench.ai)

## Task Format

Tasks are defined in YAML with clear success criteria:

```yaml
task_id: "SMS-001"
level: 1
category: "Basic Information Retrieval"
channel: "SMS"
difficulty: "easy"

input:
  from: "+15551234567"
  content: "What time is it in Tokyo?"

success_criteria:
  - type: "response_time"
    max_seconds: 30
  - type: "content_accuracy"
    requires: "correct timezone conversion"
  - type: "format"
    requires: "human-readable time format"

metadata:
  estimated_duration: "10s"
  tags: ["timezone", "information-retrieval"]
```

## Task Dataset

This repository contains the task definitions. Browse `tasks/` to see all benchmark scenarios.

Each task is carefully designed with:
- **Clear inputs**: Exact message content and context
- **Success criteria**: Objective evaluation rubrics
- **Human baselines**: Expected human performance
- **Complexity factors**: What makes each task challenging

## Results & Leaderboard

View live results and compare AI assistants at [humanbench.ai](https://humanbench.ai)

## Contributing

We welcome contributions! See [CONTRIBUTING.md](docs/contributing.md) for guidelines.

- 📝 **Add tasks**: Propose new realistic scenarios
- 📊 **Improve criteria**: Better evaluation rubrics
- 🐛 **Fix issues**: Report problems with existing tasks

## Citation

If you use Human-Bench in your research, please cite:

```bibtex
@misc{humanbench2025,
  title={Human-Bench: A Benchmark for Multi-Modal Personal AI Assistants},
  author={American Productivity Company},
  year={2025},
  url={https://github.com/american-productivity-company/human-bench}
}
```

## License

Human-Bench is released under the MIT License. See [LICENSE](LICENSE) for details.

---

**Built with ❤️ by [American Productivity Company](https://righthand.ai)**
