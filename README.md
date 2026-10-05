# AutoAlgo — Autonomous Algorithm Optimization Skill

[![GitHub stars](https://img.shields.io/github/stars/zxxr1113/autoalgo?style=social)](https://github.com/zxxr1113/autoalgo/stargazers)
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

`autoalgo` is a Codex and Agent Skills-compatible workflow for autonomous
algorithm optimization without drifting into case-by-case tuning.

It is designed for research where an agent reads literature, changes an
algorithm, runs expensive experiments, attributes gains and regressions, and
must decide when to continue, pivot, or stop. The central principle is:

> Autonomous research should accumulate mechanistic understanding, not merely
> accumulate benchmark points.

If this workflow improves a real optimization study, please star the repository
and share the problem class where you used it. Evidence from actual research
runs is especially valuable.

## What makes it different

- **Research contract before autonomy.** Goal, metrics, correctness, timeout,
  evaluation cohort, initial direction, and budget are agreed before exploration.
- **Literature and mechanism first.** New directions begin from prior work or a
  causal account of the measured bottleneck.
- **No benchmark overfitting.** Individual cases diagnose bugs and mechanism
  boundaries; they are not a training set for magic numbers and special cases.
- **Batch validation after meaningful changes.** The default rhythm is
  attribution → code → 1–2 smoke cases → a predefined parallel batch.
- **Quality and prototype runtime are separated.** A slow prototype can reveal
  a valuable algorithmic direction; a tiny cheap gain can still be unimportant.
- **Attribution before iteration.** Aggregate gains, regressions, runtime,
  failures, and timeouts are explained before another idea is added.
- **Direction-level decisions.** The workflow distinguishes a failed
  implementation, a failed parameterization, and evidence against the core idea.
- **Reproducible evidence.** It records source, inputs, commands, environments,
  metrics, validity checks, profiling fields, resource use, and evidence limits.

## Suitable research problems

- search, planning, scheduling, and combinatorial optimization;
- graph algorithms and dynamic data structures;
- compiler passes and program optimization;
- SAT/SMT, theorem proving, and proof-backed transformations;
- numerical and scientific-computing kernels;
- candidate generation, ranking, pruning, caching, and incremental algorithms;
- quality/runtime tradeoff studies over heterogeneous benchmark corpora.

The workflow is most useful when evaluation is mechanical but expensive, several
algorithmic directions are plausible, and weak experimentation can easily fit a
small development set.

## Install

Using the open Agent Skills CLI:

```bash
npx skills add zxxr1113/autoalgo --skill autoalgo -g -a codex -y
```

Or clone it directly:

```bash
git clone https://github.com/zxxr1113/autoalgo.git ~/.codex/skills/autoalgo
```

Start with a prompt such as:

```text
Use $autoalgo to investigate a faster candidate-evaluation algorithm.
Before autonomous work, help me agree on the quality target, runtime target,
initial direction, timeout, evaluation batch, correctness checks, and budget.
```

## Worked example

[Speeding up ABC `&scorr`](examples/scorr-speed-optimization.md) demonstrates the
generic workflow on an EDA algorithm. It covers profiling, cohort selection,
paired timing, work-count attribution, timeout policy, and mechanism-level
continue/pivot/stop decisions without publishing experimental results.

## Repository structure

```text
autoalgo/
├── SKILL.md
├── agents/openai.yaml
├── examples/
│   └── scorr-speed-optimization.md
└── references/
    ├── research-record.md
    └── experiment-workflow.md
```

`SKILL.md` contains the research policy. The references define a reusable
experiment workflow and research record. The example applies them to a concrete
EDA speed-optimization problem.

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

Representative cases are deliberately short-lived. If the agent keeps adjusting
thresholds or policies around them, the workflow requires it to recover a general
mechanism before proceeding.

## 中文简介

`autoalgo` 是一个面向通用算法优化的自主科研 Skill，适用于搜索、求解器、
编译优化、图算法、科学计算、EDA 等具有可重复实验指标的研究问题。它强调文献与
机制、批量验证、因果归因和可泛化性，避免 Agent 围绕少数 benchmark 不断调整
阈值、重试策略和特殊分支。

默认节奏是：归因分析 → 修改算法 → 运行一两个典型 case 排错 → 尽快并行运行
预先定义的批量 case → 判断继续、优化、转向或停止。

## Contributing

Reports from real algorithm-research runs are the most useful contribution. See
[CONTRIBUTING.md](CONTRIBUTING.md) to share a workload, failure mode, or research
rule that improved agent behavior.

## License

MIT
