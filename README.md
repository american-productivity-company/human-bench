# Human-Bench 🤖→🧑

**A benchmark for human-like capability from virtual humans made of AI Agents.**

Human-Bench evaluates AI agents on realistic, multi-modal communication tasks that mirror how humans actually interact with human employees—across SMS, email, and voice calls, with context that spans days or weeks.

## Why Human-Bench?

Existing benchmarks test coding ability (SWE-bench), general reasoning (GAIA), or tool use (τ-bench). But none evaluate what makes a truly useful human:

- 📱 **Multi-modal communication** (SMS, Email, Voice, Slack, Teams)
- 🔗 **Cross-channel context** ("About that email I sent..." during a phone call)
- ⚡ **Priority management** (handling interruptions gracefully)
- 📅 **Long-term coherence** (planning a wedding over weeks)
- 🎯 **Human-like interaction patterns** (not just Q&A)
- 🔒 **Security & Privacy** (resisting unauthorized access attempts)
- 👥 **Team coordination** (managing multiple users and delegation)

## How It Works

**Human-Bench is a hosted benchmark service.** We handle all testing and evaluation.

1. **Register your AI assistant** at [human-bench.com](https://human-bench.com)
2. **Provide contact info**: Your persona's phone number, email, and name
3. **We run the tests**: We send SMS, emails, and phone calls to your assistant
4. **Get your score**: See detailed results and compare on the public leaderboard

No setup required - just register and test!

## Benchmark Structure



**🔗 Test Your Assistant**: [humanbench.ai](https://human-bench.com)

## Task Format

Tasks are defined in YAML with clear success criteria:

```yaml
example_goes_here
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
