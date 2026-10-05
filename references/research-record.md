# Research Record

Adapt this structure to the project's existing authoritative report. Do not create duplicate handoff documents merely to satisfy the template.

## Research contract

- Problem, scope, and correctness boundary
- Baseline and exact quality metric
- Runtime or resource metric
- Quality and runtime expectations
- Initial timeout and evaluation cohort
- Accepted initial direction and causal hypothesis
- Relevant literature and adaptation assumptions
- Files or behavior that may change and evaluation components that must remain fixed
- Autonomous budget and discussion checkpoint
- Execution hosts and concurrency limits

## Direction and hypothesis

- Mechanism problem and existing evidence
- Testable hypothesis and expected generalization conditions
- Changed variable, fixed conditions, and control
- Observation that would support or refute the hypothesis
- For an A+B chain: capability supplied by A, limitation preventing A from helping alone, how B removes it, and the predicted combined effect

## Experiment identity

- Source revision and dirty patch
- Build toolchain, flags, binary identity, and host
- Input manifest and content identities
- Complete command, arguments, environment, timeout, and workers
- Correctness or proof policy
- Raw result location and parser version
- Experiment stage: representative smoke cases or predefined batch
- CPU load, memory, scratch, competing jobs, and timing interference

## Validity and results

- Total, completed, failed, timed-out, malformed, and excluded cases
- Correctness outcomes reported separately from process exit status
- Primary quality metric with per-case normalization when appropriate
- Better/equal/worse distribution and important tails
- Runtime distribution with ratio direction stated explicitly
- Relevant generated, attempted, proved, selected, or committed work counts
- Phase times or scaling counters tied to the hypothesis
- Instrumentation fields added and their measurement overhead

## Attribution

- Direct observations
- Causal explanation and supporting controls or ablations
- Sources of gains, regressions, runtime, failures, and timeouts
- Alternative explanations and confounders
- Applicability limits, counterexamples, and unvalidated regions
- Attribution state: established, partial, or unresolved, with reasons

## Decision

- Does the evidence concern the implementation, parameterization, or core direction?
- Continue, investigate attribution, optimize speed, pivot, return to discussion, or stop
- If continuing: mechanism signal, batch evidence, and causal chain for the next experiment
- If stopping: structural limitation and evidence strength
- Usage budget consumed and limitations of its measurement

## Run conclusion

- Results that survived batch validation
- Mechanistic knowledge established
- Failed hypotheses worth preserving
- Remaining uncertainty
- Why work stopped
- Next directions and expected effort
