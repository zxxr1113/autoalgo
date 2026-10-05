# Algorithm Experiment Workflow

Use the project's own commands, evaluators, and schemas when they exist. This
reference defines general invariants for algorithm optimization studies with
mechanical but potentially expensive evaluation.

## Define the comparison

Record the exact baseline, candidate, input corpus, seed policy, timeout, worker
count, validity checks, and metric definitions. Keep the evaluator and validity
rules fixed during a comparison. If the protocol must change, establish a new
matched baseline.

Choose representative smoke cases for debugging and mechanism inspection.
Choose the batch before examining candidate outcomes. Cover relevant input
families, sizes, baseline costs, structural properties, and known hard cases. A
historically completing corpus is a convenience, not a guarantee of future
completion or correctness.

## Separate optimization quality from validity

Define the domain's non-negotiable validity boundary: exact correctness,
equivalence, feasibility, numerical tolerance, proof obligations, invariants, or
another explicit contract. Report each validity outcome separately from process
exit status.

Quality metrics belong outside this guard. Examples include objective value,
solution quality, approximation error, accuracy, throughput, memory, latency,
model size, graph size, or stage-specific gain. Never hide a validity failure in
a weighted aggregate.

Preserve assertions and proof obligations. Fix violated invariants instead of
silencing them or adding a fallback that hides the failure.

## Report distributions and coverage

Pair the same input identities. Do not impute missing values or compare unlike
valid populations without stating the selection effect.

When cases have equal weight, normalize each case first and then compute mean
and median. Also report better/equal/worse counts, totals as supporting evidence,
coverage, exclusions, and important tails. State the numerator, denominator,
and ratio direction for every headline metric.

Aggregate improvements with local regressions are research evidence. Attribute
their structural differences instead of forcing zero regression through
per-case policies.

## Profile the mechanism

Select counters that test the causal hypothesis. Depending on the algorithm,
useful data may include:

- candidate generation, filtering, evaluation, selection, and commit counts;
- queue, frontier, relaxation, expansion, proof, or solver work;
- cache hits, misses, invalidations, and memory footprint;
- search width, depth, branching, support size, and accepted gain;
- time in parsing, preprocessing, core computation, reconstruction, and cleanup;
- asymptotic work counts and the variables expected to control them.

Do not copy every available field into the report. Record the fields needed to
understand the mechanism and preserve raw data for later questions.

## Use parallelism without corrupting timing

Inspect the host before launching. Choose workers from available CPUs, actual
busy cores, memory per job, scratch capacity, and project limits. Parallelize
independent cases aggressively when safe.

Use high-concurrency batches for fast quality and work-count discovery. Confirm
runtime claims with control and candidate on the same host under comparable
low-interference load. Keep compiler, ISA flags, binary provenance, input
identity, timing boundary, runtime environment, and toolchain matched. Do not
combine timings from different machines into one speedup.

## Preserve provenance

For every measured run, retain enough information to reproduce:

- source revision and dirty patch;
- compiler/interpreter, flags, dependencies, and executable identity;
- input manifest and content identities;
- full command, configuration, seed, and environment;
- evaluator, validity checker, and parser identity;
- host, workers, timeout, and load conditions;
- raw outputs and validity artifacts.

Keep scratch disposable only after required evidence has been preserved. Never
overwrite a frozen control with the current candidate.
