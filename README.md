# Research Auto for EDA Algorithm Optimization

[![GitHub stars](https://img.shields.io/github/stars/zxxr1113/research-auto?style=social)](https://github.com/zxxr1113/research-auto/stargazers)
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

`research-auto` is a Codex skill for running autonomous algorithm research without drifting into case-by-case tuning.

It was developed from a real EDA optimization workflow: logic synthesis and sequential optimization experiments where quality, runtime, proof status, profiling, corpus bias, and reproducibility all matter. The central idea is simple:

> Autonomous research should accumulate mechanistic understanding, not merely accumulate benchmark points.

If this workflow helps your research, please star the repository and share the EDA workload where you tried it. Real experiment feedback is especially valuable.

## What makes it different

- **Literature and mechanism first.** New directions begin from prior work or a clear causal analysis.
- **Quality value is judged independently from prototype speed.** A slow prototype can still reveal a valuable direction.
- **No benchmark overfitting.** Individual circuits diagnose bugs and bottlenecks; they are not a training set for magic numbers and special cases.
- **Batch validation after each meaningful change.** The default rhythm is attribution → code → 1–2 smoke cases → a predefined parallel batch.
- **Attribution before iteration.** Aggregate gains, regressions, runtime, and timeouts are explained before another idea is stacked on top.
- **Direction-level decisions.** The skill distinguishes a failed implementation from a failed parameterization and from evidence against the core idea.
- **Compute-aware execution.** It uses safe server parallelism for discovery and low-interference paired runs for timing claims.
- **Reproducible EDA evidence.** It records source, binary, inputs, commands, proof policy, workers, timeouts, metrics, and profiling fields.

## Typical use cases

- logic rewriting and resubstitution;
- cut enumeration and candidate evaluation;
- technology mapping;
- combinational or sequential optimization;
- SAT-backed transformation and proof workflows;
- cache, representation, and data-structure research;
- quality/runtime tradeoff studies across circuit corpora.

The workflow also applies to other algorithm research with mechanical evaluation and expensive batch experiments.

## Install

Using the open Agent Skills CLI:

```bash
npx skills add zxxr1113/research-auto --skill research-auto -g -a codex -y
```

Or clone it directly:

```bash
git clone https://github.com/zxxr1113/research-auto.git ~/.codex/skills/research-auto
```

Then start with a prompt such as:

```text
Use $research-auto to investigate a new cut-evaluation algorithm.
Before autonomous work, help me agree on the quality target, runtime target,
initial direction, timeout, batch, correctness checks, and research budget.
```

## Repository structure

```text
research-auto/
├── SKILL.md
├── agents/openai.yaml
└── references/
    ├── research-record.md
    └── eda-experiment-workflow.md
```

`SKILL.md` contains the research policy. The references define a reusable experiment record and EDA-specific validation guidance.

## Core experiment loop

```text
literature / mechanism analysis
            ↓
      causal hypothesis
            ↓
       coherent change
            ↓
  1–2 representative smoke cases
            ↓
 predefined parallel batch
            ↓
 attribution of gains, losses, time, failures
            ↓
 continue / optimize / pivot / stop
```

Representative cases are deliberately short-lived. If the agent keeps adjusting thresholds or policies around them, the workflow requires it to stop and recover a general mechanism before proceeding.

## 中文简介

`research-auto` 是一个面向 EDA 算法优化的自主科研 skill。它强调文献与机制、批量验证、因果归因和可泛化性，避免 agent 围绕少数 benchmark 不断调整阈值、重试策略和特殊分支。

默认研究节奏是：归因分析 → 改代码 → 跑一两个典型 case 排错 → 尽快并行跑预先定义的批量 case → 判断继续、优化、转向或停止。

## Contributing

Real EDA experiment reports are the most useful contribution. See [CONTRIBUTING.md](CONTRIBUTING.md) to share a workload, a failure mode, or a rule that improved research behavior.

## License

MIT
