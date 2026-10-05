# EDA Experiment Workflow

Use the repository's own commands and schemas when they exist. This reference captures the invariants that commonly matter in logic synthesis, rewriting, resubstitution, mapping, SAT-backed optimization, and sequential optimization.

## Define the comparison

Record the exact baseline, candidate, input corpus, seed policy, timeout, worker count, proof settings, and metric definitions. Keep the evaluator and correctness checks immutable during a comparison. If the evaluation protocol must change, establish a new matched baseline.

Choose representative smoke cases for fast debugging and mechanism inspection. Choose the batch before examining candidate outcomes. Cover relevant circuit families, sizes, baseline costs, structural properties, and known hard cases. Treat a historically completing corpus as a convenience, not a guarantee of future completion or correctness.

## Separate optimization quality from correctness

Optimization metrics may include final node or gate count, area, delay, depth, register count, power proxies, or stage-specific gain. Correctness is a guard, not another weighted metric.

For combinational transformations, use the project's independent combinational equivalence check. For sequential transformations, use the required sequential equivalence or property check with explicit timeout and status. Report PASS, timeout, unknown, assertion, parser error, and interface mismatch separately. Never infer equivalence from process exit status alone.

Preserve proof obligations and assertions. Fix violated invariants rather than silencing them or adding a fallback that hides the failure.

## Report distributions and coverage

Pair the same input identities. Do not impute missing values or compare unlike PASS populations without stating the selection effect.

For equal-weight circuit reporting, normalize each circuit first and then compute mean and median. Also report better/equal/worse counts, totals as supporting evidence, coverage, exclusions, and important tails. State the numerator, denominator, and ratio direction for every headline metric.

Aggregate improvements with local regressions are research evidence. Attribute their structural differences instead of forcing zero regression through per-circuit policies.

## Profile the mechanism

Select counters that test the causal hypothesis. Depending on the algorithm, useful data may include:

- candidate generation, filtering, proof, selection, and commit counts;
- cut enumeration, truth-table, simulation, SAT, rewriting, cleanup, and graph-update time;
- cache hits, misses, invalidations, and memory footprint;
- search width, depth, fanout, support size, MFFC size, and accepted gain;
- asymptotic work counts and the variables expected to control them.

Do not copy every available field into the report. Record the fields needed to understand the mechanism and preserve raw data for later questions.

## Use parallelism without corrupting timing

Inspect the host before launching. Choose workers from available CPUs, actual busy cores, memory per job, scratch capacity, and project limits. Parallelize independent circuit runs aggressively when safe.

Use high-concurrency batches for fast quality and work-count discovery. Confirm runtime claims with control and candidate on the same host under comparable low-interference load. Keep compiler, ISA flags, binary provenance, input identity, timing boundary, and toolchain matched. Do not combine timings from different machines into one speedup.

## Preserve provenance

For every measured run, retain enough information to reproduce:

- source revision and dirty patch;
- compiler, flags, dependencies, and binary hash;
- input manifest and hashes;
- full command and environment;
- parser and evaluator identity;
- host, workers, timeout, and load conditions;
- raw outputs and correctness artifacts.

Keep scratch disposable only after required evidence has been preserved. Never overwrite a frozen control with the current candidate.
