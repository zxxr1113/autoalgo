# Worked Example: Speeding Up ABC `&scorr`

This illustrative example shows how `research-auto` organizes a runtime
optimization study for ABC sequential correlation reduction. It describes the
research method and decision rules without claiming unpublished measurements.

## Research question

Can `&scorr` be made substantially faster on expensive sequential circuits
without weakening correctness or losing the reductions produced by the agreed
baseline configuration?

The goal is a general algorithmic improvement. A patch that only speeds up a
few named circuits or changes limits until the evaluation set looks better does
not answer the question.

## Experiment contract

Before autonomous work begins, the researcher and agent agree on:

| Field | Example agreement |
| --- | --- |
| Primary objective | Reduce end-to-end `&scorr` runtime on a frozen expensive-case cohort |
| Quality expectation | Preserve the agreed output-quality metrics and explain every regression |
| Correctness | Validate every completed product with the established independent equivalence policy |
| Cohort selection | Choose larger cases from baseline input size and runtime before seeing candidate results |
| Timing | Compare baseline and candidate on the same host, with the same command boundary and comparable load |
| Repetition | Use repeated low-interference paired runs for the final speed claim |
| Initial timeout | Define one timeout before the first batch |
| Timeout policy | Analyze completed cases first; use one 2× rerun only when the speed/quality signal justifies it |
| Research budget | Agree on the autonomous budget and escalation point |

Small cases are useful for correctness and integration checks. They cannot
establish the main speed claim when startup and measurement noise dominate.

## Attribute the runtime before optimizing

Add observation fields without deleting or changing existing ones. Separate at
least these costs when the implementation permits it:

- graph preparation and normalization;
- simulation and signature maintenance;
- candidate generation and filtering;
- SAT or proof work;
- relation, class, or worklist maintenance;
- graph reconstruction and cleanup.

Record work counts alongside wall time. A faster run that silently performs less
logical work is a quality change until shown otherwise.

## Mechanism hypotheses

The first experiments should test a small number of structural hypotheses:

1. **Repeated invariant construction.** A dominant object may be rebuilt even
   when its inputs have not changed. Reuse it with an explicit validity rule.
2. **Representation cost.** A relation, class, or candidate structure may incur
   avoidable scans or poor locality. Replace the data structure so the same work
   has lower asymptotic or constant cost.
3. **Incremental maintenance.** A full recomputation may follow a local graph
   update. Maintain the affected frontier and invalidate only dependent state.

Each hypothesis predicts which phase time and work counter should change. If the
predicted counter does not move, an apparent wall-time gain needs another
explanation before more code is added.

## Efficient experiment loop

1. Profile the frozen baseline batch at high safe parallelism.
2. Select one mechanism from the attribution, not one troublesome circuit.
3. Implement one coherent change with assertions on ownership and invalidation.
4. Run one or two representative cases to catch crashes, stale state, and gross
   quality changes.
5. Run the predefined batch immediately when server capacity permits.
6. Preserve timeouts, failures, quality regressions, and per-phase counters.
7. Confirm promising speedups with paired, low-interference repetitions on the
   same server.
8. Decide whether to continue, redesign, pivot, or stop from the mechanism-level
   evidence.

## Example decision table

| Observation | Attribution | Decision |
| --- | --- | --- |
| Large paired speedup; work counts and quality preserved | The implementation removes overhead while preserving algorithmic work | Continue to broader validation |
| Phase time falls where predicted, but total runtime barely moves | The mechanism is real but not a current end-to-end bottleneck | Record it and move to the dominant phase |
| A few small cases improve; expensive cohort is flat | Startup or noise likely dominates the apparent gain | Do not polish the variant |
| Runtime improves because candidate/proof counts fall | The patch changed algorithmic effort | Treat as a quality/runtime tradeoff and explain the lost work |
| Median improves but several large cases regress | Aggregate speedup hides a scaling or invalidation problem | Analyze the regressing family before continuing |
| Many timeouts and no convincing completed-case gain | The implementation path is weak | Stop instead of adding retries or special limits |
| Strong completed-case gain with a small timed-out tail | Direction remains promising | Use the agreed one-time 2× timeout rerun |

## What the agent must not do

- add circuit-name branches or per-case parameter tables;
- tune magic thresholds against the evaluation cohort;
- remove expensive correctness work and call the result an implementation speedup;
- report only the fastest run or only an aggregate mean;
- mix timings from different hosts or different command boundaries;
- keep stacking micro-optimizations without re-profiling the dominant cost;
- use retries or rescue paths to hide a mechanism that does not generalize.

## Minimal research record

```text
Direction: &scorr runtime optimization
Baseline: <commit, binary, command, host, compiler, input identities>
Hypothesis: <repeated work or scaling mechanism>
Change: <commit and precise algorithm/data-structure change>
Cohort: <predeclared selection rule and cases>
Correctness: <independent policy and outcomes>
Quality: <aggregate and per-case deltas>
Runtime: <paired repetitions and distributions>
Attribution: <phase times, work counts, scaling variables>
Timeouts/failures: <retained outcomes and optional 2x rerun>
Evidence strength: <confirmed / suggestive / contradicted / unknown>
Decision: <continue / redesign / pivot / stop>
Next discriminating experiment: <test that separates competing explanations>
```

The result is valuable even when an implementation is abandoned: the record
identifies which phase dominates, which proposed mechanism actually changed the
work, and which direction should receive the next research budget.
