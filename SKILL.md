---
name: autoalgo
description: "Run bounded, mechanism-first autonomous research for algorithm optimization. Use when the user wants an agent to investigate literature-backed directions, implement prototypes, run controlled batches, attribute quality and runtime changes, and decide whether to continue, pivot, or stop. Applies across search, solvers, compilers, graph algorithms, scientific computing, and other mechanically evaluated algorithms. Do not use for an ordinary one-off benchmark, bug fix, or literature lookup."
---

# AutoAlgo — Autonomous Algorithm Optimization Skill

Use this skill to turn an open-ended optimization goal into a bounded research program. Preserve the project's own correctness rules, metric definitions, experiment tools, resource limits, and authoritative report.

## Establish the research contract

Before unattended exploration, agree with the user on:

- the research question and scope;
- the quality metric, baseline, and expected improvement;
- the runtime or resource metric and expected range;
- correctness guards and immutable evaluation rules;
- the initial experiment timeout and evaluation cohort;
- the autonomous work or usage budget and the checkpoint for returning to discussion;
- the initial direction and why it deserves investment.

Explain the initial direction as a causal hypothesis: what mechanism is missing or wasteful, why the proposed change should affect it, what evidence would support or refute it, and what remains uncertain. Start implementation only after the user accepts this direction. During the authorized run, the agent may pivot when evidence warrants it, provided the goal, method boundaries, and budget remain unchanged.

Treat the budget as a ceiling for unsupervised work, not a target to consume. Keep enough budget for attribution and a useful final report. Stop new research when the authorized budget is reached; do not extend it merely because a direction looks promising.

## Start from literature or a clear mechanism

For a new problem, search and read relevant primary literature, algorithm descriptions, and useful author implementations before proposing directions. Determine what existing methods solve, the assumptions they require, how the current setting differs, and which properties must be revalidated after adaptation.

If the mechanism and solution are already clear from reliable analysis, proceed without ceremonial literature search. Return to targeted literature review when a new mechanism, assumption, or knowledge gap appears.

## Optimize mechanisms that can generalize

Every optimization needs a generalizable mechanism. A score increase on the development cases is not by itself evidence of a useful algorithm.

Prefer changes to algorithm structure, representation, complexity, data structures, proof strategy, or a measured bottleneck. State the expected class of affected inputs and the conditions under which the change should help. When validation is limited, say that generalization is not yet established.

Do not repeatedly tune thresholds, weights, ordering, retry counts, or special cases until a few examples improve. Avoid rescue and retry branches as a default research strategy. Do not introduce heuristics, especially magic-number heuristics, unless the user explicitly authorizes heuristic research. A pruning rule based on dominance, equivalence, infeasibility, or a sound bound is structurally different from an empirical score cutoff.

Use individual cases to find bugs, bottlenecks, broken invariants, and mechanism boundaries. Before changing code because of a case, explain the general condition it reveals and how the proposed change addresses that condition.

## Use a batch-first experiment rhythm

Follow this default loop:

1. Analyze existing evidence and form an attribution hypothesis.
2. Make one coherent algorithmic change, or a tightly coupled A+B change with an explicit causal chain.
3. Run one or two representative cases to catch implementation errors and confirm that the intended mechanism is exercised.
4. Promptly run a predefined batch and analyze the full distribution.

Representative cases are smoke tests and diagnostic probes. They do not establish overall value or generalization. Do not keep modifying the method on those cases until they look good.

When server resources and project rules permit, run the predefined batch in parallel after every meaningful algorithm change. Select the batch before seeing candidate results, based on coverage, input classes, scale, and known feasibility. Retain failures, timeouts, and regressions. Do not reshape the cohort around candidate outcomes.

Purely mechanical build fixes may be combined with the next meaningful batch when a separate run would add no information.

## Use available compute efficiently

Before building or launching experiments, inspect the execution host, available and busy CPUs, load, memory, scratch space, existing jobs, and project concurrency limits. Use high parallelism when there is safe headroom. Do not mechanically retain a conservative default, starve other authorized work, exceed memory or scratch capacity, or launch experiments without discriminating value.

Record the host, worker count, timeout, and relevant load conditions. High-concurrency batches are useful for discovering quality and mechanism signals, but contention can invalidate runtime conclusions. Confirm speed claims with paired control and candidate runs on the same host, inputs, timing boundary, and comparable low-interference load.

## Evaluate quality before optimizing speed

Judge quality against the agreed target. If quality reaches the target, the direction has research value even when the prototype is extremely slow. Continue probing the quality ceiling while the current mechanism still has clear, principled headroom. Turn to complexity, data structures, and measured runtime bottlenecks when further quality progress requires a new core idea.

A tiny quality gain is not made important by having almost no runtime cost. Conversely, do not reject a high-quality direction merely because its first implementation is slow.

If aggregate quality improves materially, retain the candidate even when some cases regress. Attribute both the gains and the regressions: the contrast may reveal applicability conditions or the next research question. Do not eliminate every regression with case-specific patches. Correctness failures remain unacceptable.

An intermediate change A need not improve the final metric on its own when the mechanism requires A+B. Before investing in B, explain what capability A creates, why the current pipeline cannot exploit it, how B removes that limitation, and what observable result would validate the chain.

## Handle timeouts in stages

Agree on the initial timeout before the experiment and prefer cases known to finish under the baseline conditions.

If the candidate causes timeouts, first analyze the completed cases, while reporting coverage and selection limits. Do not present the completed subset as the full cohort. If completed cases show high quality value, rerun only the timed-out cases once at twice the initial timeout, subject to the research budget. Preserve the original timeout outcomes and keep the budgets distinct. If quality value is low and timeouts are widespread, stop the current implementation path instead of repeatedly extending timeouts.

## Attribute results before building on them

After an aggregate improvement, complete attribution before stacking another idea. Run the discriminating ablation, matched control, stage counter, or cross-case test needed by the actual ambiguity.

Separate observations from explanations. Check source and binary identity, inputs, parameters, correctness status, metric semantics, exclusions, and resource budgets. State which change produced which effect, the evidence supporting the causal explanation, plausible alternatives, applicability limits, and remaining uncertainty.

When existing profiling cannot answer the question, add the necessary fields and parser support. Preserve every existing field and its meaning. Record new field definitions and check whether instrumentation affects the result or timing.

## Decide whether a direction deserves more work

Before continuing or abandoning a direction, perform direction-level attribution. Determine:

- whether the implementation faithfully represents the hypothesis;
- whether the expected mechanism actually activates;
- where quality gains, regressions, runtime cost, failures, and timeouts originate;
- whether the batch distribution matches the mechanism;
- which confounders or alternative explanations remain;
- whether the evidence concerns one implementation, one parameterization, or the core direction.

Continue when there is a mechanism signal, batch evidence relevant to the goal, and a causal argument for the next experiment. Stop an implementation when a structural limitation is established. Abandon the whole direction only with stronger evidence that a faithful implementation has insufficient value on a representative batch, or that remaining work consists mainly of case tuning, magic numbers, retries, or patches without a generalizable basis.

When evidence cannot distinguish these possibilities, record the direction as unresolved and design one discriminating measurement or ablation. Do not substitute incremental tuning for a decision.

## Keep reproducible research records

Use the project's authoritative report rather than creating session handoffs. Read [the research record](references/research-record.md) when preparing experiments or reporting results. For cohort selection, validity, profiling, provenance, and timing guidance, read [the experiment workflow](references/experiment-workflow.md).

Keep raw data separate from interpretation. Record negative results and evidence limits. At the end of the authorized run, report verified effects and attribution, failed hypotheses, unresolved uncertainty, budget limitations, and the most defensible next directions.

This skill does not authorize production integration, default activation, control of other tasks, or changes outside the agreed research scope.
