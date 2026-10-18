# Methods and interpretation

The complete implementation is in Notebook 01. Notebook 02 embeds the original timed-study code and should be used only for manuscript reproduction.

## Search

A chromosome has one legal time-room pair per event. Legal domains enforce cohort off days, teaching hours, protected breaks, lecturer and room unavailability, type and capacity. Remaining H counts pairwise cohort, lecturer and room clashes. The independent validator checks all hard requirements plus event completeness and malformed records.

The population has 24 candidates by default. Uniform crossover chooses each gene from either parent with probability 0.5. Mutation resamples a legal gene with probability min(1, 2/n). Binary tournament selection and steady-state worst-member replacement are used. A three-percent random population admission allows exploration. These are starting settings, not tuned state-of-the-art parameters.

Scarcity-ordered repair first processes meetings with fewer legal placements. It tries inherited genes before randomly ordered alternatives. It may leave residual conflicts when no immediate legal placement exists. Lamarckian repair inherits the phenotype; Baldwinian repair scores a temporary phenotype and retains its genotype. Baldwinian fitness can be stochastic because repair ordering is random.

Static penalty selection uses 100H+S. The coefficient is configurable and is not a proven dominance bound. Feasibility-first selection compares (H,S). Every arm keeps a separate (H,S) archive of evaluated phenotypes. This archive convention matches the original study.

## Soft quality

S = 3G + 2O + M + R.

- G counts empty teaching slots between a cohort's first and last daily meeting, excluding lunch.
- O counts cohort-day meeting hours above four.
- M counts meetings beyond the first for a cohort-module-day.
- R counts distinct rooms above two for a cohort-module offering.

The weights are synthetic preferences, not validated satisfaction measures. A feasible schedule can have a positive soft score. The score has no common scale with ITC or unrelated timetabling benchmarks.

## Exact baseline

Notebook 01 uses a binary event-time-room model with a zero objective and real legal room domains, including capacities and unavailability. A validated incumbent proves feasibility even if the solver reaches a limit. Infeasibility is reported only for an empty domain or a solver infeasibility status. No incumbent without a certificate is reported as unknown. A zero objective does not establish a minimum S.

## Reproducibility

Fixed-evaluation budgets count complete candidate scores, with repair probes recorded separately; these are not identical primitive workloads. Timed budgets are soft and host-dependent, with initialisation included but completed before stopping. Notebook 01 shuffles method order by seed. Notebook 02 preserves the original fixed order.

The original snapshot contains 120 outcomes on one constructed constraint instance. Changing only enrolment random seeds while every room still fits would not create distinct effective constraint problems. Bootstrap intervals over runs describe randomness conditional on the workload. They do not support general claims across universities. Failed runs retain their feasibility denominator and are excluded only from explicitly conditional quality summaries.

## Curriculum alignment

Unit 4: representation, population diversity, selection, crossover, mutation and replacement. Unit 5: constrained formulation, penalties, feasibility rules, repair, Lamarckian/Baldwinian strategies, repeated runs, cost accounting and honest uncertainty.

## References

- Deb (2000), https://doi.org/10.1016/S0045-7825(99)00389-8
- Müller et al. (2025), https://doi.org/10.1007/s10951-023-00801-w
- Davison et al. (2025), https://doi.org/10.1007/s10951-024-00817-w
- Zhu et al. (2026), https://doi.org/10.1016/j.asoc.2025.114150
- SciPy MILP API, https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.milp.html

Public ITC benchmark instances are referenced but not bundled or evaluated. The manuscript article's wider bibliography remains available in its separate document.
