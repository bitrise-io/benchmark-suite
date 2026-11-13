# benchmark-suite

Runs every Build Hub benchmark as one **lane** per pool: one build at a time, in order
(Firefox → Signal → DuckDuckGo build → DuckDuckGo tests → Telegram Debug → Telegram Release → XcodeBenchmark → Sysbench),
optionally twice (`passes=2`, 2 builds per cell). Each job checks out a `bitrise-io/benchmark-*` repo and runs that
repo's `.github/bench` scripts, so the benchmark logic lives in the project repos.

```bash
gh workflow run lane.yml -R bitrise-io/benchmark-suite -f runner=bitrise-m6-benchmark
gh workflow run lane.yml -R bitrise-io/benchmark-suite -f runner=bitrise-m5pro-benchmark
```

Results: one artifact per job (`p<pass>-<job>-<runner>`, with summary.json, results.csv, system info and zipped logs).
Part of BPS-734; method notes in the Bitrise Benchmark Dashboard project (`benchmarking/github-actions/README.md`).
