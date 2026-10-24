# Star history: preserved upstream snapshot

This fork does not maintain an independent star-count time series. The retained
[`star-history.tsv`](star-history.tsv) and [`star-history.svg`](star-history.svg)
belong to **Dominic789654/awesome-deepseek-harness**, not
`pengpengyi92/awesome-deepseek-harness-1`. They end on **2026-08-19** and are
preserved byte for byte, including the original provenance comments and SVG
labels. The inherited “daily sample” caption describes the original design,
not a currently operating sampler in this fork.

## Maintenance decision — 2026-10-24

Retire the inherited scheduled workflow in this fork; retain the upstream data,
chart and script for reference. This is a contribution/reference fork, not an
exact mirror: at inspection it had one independent documentation commit updating
the dsh-quant entry, and no established fork-specific star-history series. There
is no demonstrated need to run daily collection here. This is a scoped
maintenance decision, not a declaration that the entire repository is abandoned.

The workflow has been moved from `.github/workflows/star-history.yml` to
[`docs/archive/star-history.workflow.yml`](../docs/archive/star-history.workflow.yml)
without changing its contents. Outside `.github/workflows`, it is reference
material rather than an executable GitHub Actions workflow. The retirement takes
effect when this change reaches the default branch; opening a PR alone does not
stop its existing schedule. No workflow was re-enabled, dispatched or represented
as successfully sampling during this repair. The separate PR-validation workflow
is unaffected.

## Evidence checked

All observations below are a point-in-time audit on 2026-10-24, before this change.

| Item | Observation | Source |
| --- | --- | --- |
| Repository relationship | `fork: true`; both `parent` and `source` are `Dominic789654/awesome-deepseek-harness`; fork created 2026-08-17 | [Repository API](https://api.github.com/repos/pengpengyi92/awesome-deepseek-harness-1) |
| Default branch | `main` at `0cfb2d5db58bdb1b51f94b41a4a543b02b21296b`; last code push 2026-09-01 | [Inspected commit](https://github.com/pengpengyi92/awesome-deepseek-harness-1/commit/0cfb2d5db58bdb1b51f94b41a4a543b02b21296b) |
| Divergence | Fork 1 commit ahead / 300 behind upstream at inspection; the independent commit updates dsh-quant documentation | [Comparison API](https://api.github.com/repos/Dominic789654/awesome-deepseek-harness/compare/main...pengpengyi92:main) |
| Current counts | Fork 0 stars; upstream 400 stars; these are current totals, not historical samples | [Fork API](https://api.github.com/repos/pengpengyi92/awesome-deepseek-harness-1), [upstream API](https://api.github.com/repos/Dominic789654/awesome-deepseek-harness) |
| Workflow state | Workflow ID `347184860`, `state: active`; the inactivity notification was a warning, not evidence of an already disabled workflow | [Workflow API](https://api.github.com/repos/pengpengyi92/awesome-deepseek-harness-1/actions/workflows/347184860) |
| Available run history | API returned 53 runs, all `schedule`, `completed` / `skipped`, spanning 2026-09-02 through 2026-10-24; page 2 was empty | [Runs API](https://api.github.com/repos/pengpengyi92/awesome-deepseek-harness-1/actions/runs?per_page=100), [earliest returned run](https://github.com/pengpengyi92/awesome-deepseek-harness-1/actions/runs/33596227805), [latest returned run](https://github.com/pengpengyi92/awesome-deepseek-harness-1/actions/runs/40067976093) |
| Latest job | `sample` was skipped, with an empty steps array and no assigned runner | [Job](https://github.com/pengpengyi92/awesome-deepseek-harness-1/actions/runs/40067976093/job/120795118004) |
| Configuration | `15 1 * * *` requests 01:15 UTC / 09:15 Asia/Shanghai; the job allows only the upstream repository; the Python default also names upstream | [Original workflow](https://github.com/pengpengyi92/awesome-deepseek-harness-1/blob/0cfb2d5db58bdb1b51f94b41a4a543b02b21296b/.github/workflows/star-history.yml), [script](../.scripts/star_history.py) |

The upstream-only condition was an intentional fork guard, as its comment and
introducing commit explain. Changing it to admit this fork without separating
the data would be unsafe. The available run history proves skipped runs, not
successful sampling; it cannot establish the status of deleted or otherwise
unavailable runs. The latest schedule was actually created at 05:52:45 UTC
(13:52:45 Asia/Shanghai), not at its requested 09:15 local time.

## Data provenance and chart use

The data, renderer, SVG and original workflow were introduced by upstream
[commit f85e9ac](https://github.com/Dominic789654/awesome-deepseek-harness/commit/f85e9ac10db6226e3fa00e105f68bd86f4a011ca)
([PR #170](https://github.com/Dominic789654/awesome-deepseek-harness/pull/170)).
The following provenance is recorded in that commit and the TSV header; the
underlying dated project logs and the original API response were not independently
recovered in this audit.

| Date | Stars | Recorded provenance |
| --- | ---: | --- |
| 2026-08-13 | 0 | Backfill: upstream creation / first commit |
| 2026-08-14 | 1 | Backfill: dated project log |
| 2026-08-17 | 118 | Backfill: dated project log |
| 2026-08-18 | 146 | Backfill: dated project log |
| 2026-08-19 | 154 | Described by upstream as its first live API sample |

August 15 and 16 have no recorded observations and remain absent. Lines between
points in the SVG do not establish observations on intervening days. No values
after August 19 are added, and none of these points are relabelled as fork data.
The first two points even predate this fork's creation.

Before correction, the English README embedded the local SVG but incorrectly
called it this repository's own daily-updated history. The Chinese README still
embedded a third-party chart for upstream. A companion documentation change
labels both as the same archived upstream snapshot. This audit does not rely on
whether the third-party chart service currently works.

Preservation checksums (SHA-256):

```text
e4fbd9c92daa855029392c0d2dd65de780d4c36a85c82af52119fc4e64d816b9  assets/star-history.tsv
db81d49aebc279198daaa69a5cff722e1dc8be39988c3adbe615badb0cd486c9  assets/star-history.svg
219b9f702bb6f62ece4712263cb9f074308ef415f201162a5a94cebcfe5702d7  .scripts/star_history.py
6d376454854f480d7f59f8ba92c7168d9f476a2d665632630860a0774661eb2c  docs/archive/star-history.workflow.yml
```

## Offline reproduction and any future restart

From the repository root, the retained renderer can reproduce the original SVG
without an API request or new sample:

```sh
STAR_HISTORY_REPO=Dominic789654/awesome-deepseek-harness python3 .scripts/star_history.py --render-only
git diff --exit-code -- assets/star-history.tsv assets/star-history.svg
```

The retained script is upstream reference code. Do not run its sampling mode
against these frozen files, and do not set `STAR_HISTORY_REPO` to the fork when
rendering them: that would mislabel upstream data. There is deliberately no
replacement scheduled or manual sampling workflow in this change.

If independent tracking becomes useful later, introduce a separate dataset and
SVG with explicit owner/repository metadata and a newly verified first sample.
Make the workflow target and Python target agree, reject mismatched dataset
identity, and keep this snapshot immutable. Do not copy this history, infer a
zero-star history from the current total, or fill the intervening dates. Before
claiming recovery, verify a completed sampling step, the recorded API target,
the resulting data commit and chart, and a subsequent scheduled run. Enabling
Actions or observing a skipped run is insufficient.

GitHub documentation: [workflow file location](https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax),
[disabling/enabling workflows](https://docs.github.com/en/actions/how-tos/manage-workflow-runs/disable-and-enable-workflows).
