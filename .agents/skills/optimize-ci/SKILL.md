---
name: optimize-ci
description: Create, review, or optimize CI pipelines and test execution for fast, trustworthy feedback. Use for slow CI, workflow changes, caching, runners, sharding, affected-test selection, local checks, or CI cost reduction. Preserve failure detection and prove improvements with real measurements.
---

# Optimize CI

Make CI as fast as possible without letting it lie. Demonstrate ruthless efficiency: remove unnecessary work, setup, serialization, and resource waste while preserving every required correctness guarantee. Optimize the critical path and total cost, not just individual commands.

Apply this to new pipelines as well as existing ones. Follow repository contracts and supported platforms. Read the general-software-engineering guidance for infrastructure and performance; use e2e-first-testing when changing test strategy or deleting tests.

## Correctness outranks speed

- Run the full required suite against the exact proposed merge result before anything reaches main, through a merge queue. Affected selection may narrow PR feedback only. If the repository lacks that gate, prepare its implementation within scope and identify any administrative setup still needed. Selective PR checks cannot substitute for full merge validation.
- Never gain speed by hiding failures: no automatic test retries, wider timeouts, skipped tests, swallowed exit codes, or weakened assertions. A check that needs a retry has a bug; investigate it and preserve evidence.
- Preserve required security checks, platforms, migrations, and failure cases. Delete tests only after proving their realistic failures remain covered. Do not start by deleting tests because CI is slow.
- Keep required gates truthful across success, failure, cancellation, and intentional no-work results. An absent or skipped required check must not silently permit a merge.
- Resolve answerable uncertainty through code, logs, official documentation, and reproductions. Confirm or deny suspected issues rather than leaving researchable questions unanswered. Name concrete access or evidence limits when resolution is blocked.

## Audit first

Inspect triggers, job dependencies, required checks, merge rules, commands, caches, runner capacity, and cancellation behavior. Trace the path from a pushed commit to its required result.

Retrieve the last 150 relevant runs, including job and step timings. If fewer exist, use all available runs and state the sample limit. For new CI, instrument initial baseline runs and mark percentile targets unverified until sufficient evidence exists.

Split each job into waiting, setup, and execution at p50 and p95. Distinguish runner queues from dependency waiting; do not invent a split the provider cannot expose. Compare equivalent cohorts: workflow, runner, PR/merge, and warm/cold caches. Keep failures and cancellations visible rather than filtering them into flattering numbers.

Find the critical path, largest time bucket, duplicate installs/builds, cache misses, and resource bottlenecks. Fix the largest measured contributor first. Save run IDs, commit SHAs, commands, workload, and raw timing evidence for repeatable comparisons.

## Default budgets

Target PR results under 2 minutes at p50 and under 3 minutes at p95, from pushed commit to completion of all required PR checks, including waiting and setup.

| Area | Target |
| --- | --- |
| Runner waiting | Under 10 seconds per job |
| Setup | Under 30 seconds per job |
| PR cache hits | Above 95% |
| Lint | Under 5 seconds |
| Typecheck | Under 5 seconds |
| Test execution | Under 60 seconds per shard |
| Local pre-push checks | Under 9 seconds |

Record repository job and critical-path budgets. Add automated checks that fail jobs exceeding their configured budget, retaining diagnostics and the underlying correctness result. Check queue budgets from provider timings when they cannot be enforced inside the runner. Do not widen budgets or truncate validation to manufacture a pass. Report unmet targets and measured constraints.

## Remove overhead and repeated work

- Cancel obsolete in-progress PR runs when a new commit lands on that branch. Scope concurrency groups so unrelated branches cannot cancel each other. Preserve merge-queue and deployment work that must complete.
- Reduce waiting through measured capacity and scheduling on existing hosted or self-hosted runners. Include short jobs: a five-second job behind a ten-minute queue is a ten-minute job. Do not mandate a runner vendor or migrate to Blacksmith.
- Seed caches from the default branch. Key them by lockfile, toolchain, OS/architecture, and other correctness inputs. For compatible JavaScript installs, evaluate caching node_modules itself, not just package downloads. Measure restore/save overhead and cold misses. Prevent incompatible restores and untrusted PR cache poisoning.
- Prefer blobless checkout (`filter: blob:none`) over shallow checkout where supported and beneficial. Fetch enough history for the correct merge base, affected graph, versioning, and other consumers. Measure checkout plus subsequent fetch costs.
- Reuse builds and artifacts for identical inputs. Run independent lint, typecheck, build, and tests in parallel while preserving real dependencies. Move migration checks and other apps' tests out of overloaded jobs when this shortens the critical path without excessive duplicate setup.

## Tool defaults require proof

For JavaScript/TypeScript repos, evaluate Oxlint for lint, Oxfmt for formatting, Bun for installs/scripts, and `bun check` for typechecking if its current supported version can check the repo. Evaluate the native TypeScript checker as fallback and tsrs locally where applicable. Verify current official documentation and installed-version support before using these candidates; never invent commands or capabilities. Other stacks need equivalent native choices based on measurements.

Before switching, run old and new tools side by side on identical source and representative deliberately invalid inputs. List relevant gaps in rules, diagnostics, plugins, formatting, resolution, lifecycle scripts, and runtime compatibility. Enable all applicable lint rules, accounting for conflicts and false positives. Prefer newer tools when measurably faster and equivalent for the repository's contract.

After proving parity, remove obsolete ESLint, Prettier, and package-manager paths instead of maintaining duplicate checks indefinitely. Retain an old tool only with a measured reason or concrete coverage/compatibility gap. Never drop checks during migration.

## Efficient, independent tests

- Measure app reload, fixture, database, and worker startup costs before increasing shards. Reuse expensive setup only when cleanup preserves independent tests.
- For Vitest, evaluate `isolate: false` when per-file reload dominates. Prove cleanup after every file, including globals, modules, mocks, timers, environment, connections, and database state as applicable. Randomize file order with recorded seeds to expose leaks. Retain isolation if independence cannot be demonstrated. Record the cleanup contract in the repo's AGENTS.md.
- Balance shards by measured duration rather than file count. Give concurrent shards independent databases and mutable resources. Match concurrency to cores and memory; avoid nested oversubscription.
- Evaluate 8-core machines and more cores before adding shards. Compare elapsed time, setup duplication, total compute, and cost. Do not purchase capacity or raise VM limits without required authorization.

## Selection and local feedback

On PRs, evaluate dependency-aware selection such as `nx affected` or `turbo --affected` where supported. Include transitive dependents and global inputs: lockfiles, shared configuration, generators, and workflows. Use the correct merge base. Fall back to full checks when the affected graph is unknown.

Challenge selection in a disposable branch/workspace: introduce a real breaking change, including a shared/transitive dependency case, and verify selected checks fail. Deliberately exercise a change the initial selection would omit; fix the graph or fallback until CI catches it. Remove the deliberate break before submission. Full merge-queue validation remains mandatory.

Install a repository-managed pre-push hook running format checks, lint, and typecheck for changed files and necessary dependents within the local budget. Resolve the actual push range, including new branches. Avoid silently modifying source during push. Provide an executable hook and reproducible setup; a line in AGENTS.md alone is insufficient. Hooks supplement authoritative CI because they can be bypassed.

## Deliver measured improvements

Use one focused PR per independently measurable change when PR delivery is requested. Validate workflow syntax and real provider execution, including affected merge gates and deliberate failure paths. Local timings cannot prove hosted CI gains.

Do everything possible within existing access and authorized resources first. If an account, secret, paid capacity, or administrator action is needed, finish concrete reviewable work, then list remaining needs together with expected monthly cost and assumptions. Do not create paid resources or change branch protection without authorization.

Report before/after PR latency and per-job waiting/setup/execution at p50 and p95, sample sizes, cache-hit rate, total compute, and monthly cost under equivalent workloads. Include total CI wall time and cost, remaining budget misses, coverage parity, and evidence links. Label estimates and unmeasured results. Keep timing and cost regression checks so later changes cannot quietly undo the improvement.
