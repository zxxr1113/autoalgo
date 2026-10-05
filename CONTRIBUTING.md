# Contributing

Contributions grounded in real research runs are welcome.

Useful reports include:

- the algorithmic problem and its correctness or validity boundary;
- the baseline, metric, corpus, timeout, and worker configuration;
- what the skill caused the agent to do;
- where the workflow prevented case tuning or weak attribution;
- where it still wasted experiments, tokens, or compute;
- the evidence supporting a proposed instruction change.

Please separate observed behavior from your explanation of its cause. Avoid adding universal rules based on a single surprising case unless the case reveals a general mechanism.

For instruction changes, keep `SKILL.md` focused and place substantial domain-specific detail in `references/`. Validate the skill before opening a pull request:

```bash
python3 /path/to/skill-creator/scripts/quick_validate.py .
```

Do not include proprietary designs, confidential benchmark data, private server paths, credentials, or licensed tool output.
