---
name: pr-review-orchestrator
description: "Given a PR diff or list of changed files, run static, security, and test-impact review in parallel and consolidate into one report. Use when the user asks for 'PR review', 'diff check', 'review these changes', or 'automated code review'. For simple single-file style feedback, defer to a plain read-through instead; for a full codebase security audit, use the built-in security-review skill instead."
allowed-tools: ["Read", "Grep", "Glob", "Bash", "Agent"]
---
# PR Review Orchestrator

## Goal
Review one change set using three specialized sub-agents. The orchestrator (you) never edits code directly — it dispatches reviewers and consolidates their findings into one report.

Adapted from a version that assumed `TeamCreate`/`TeamDelete`/peer-to-peer `SendMessage`/`TaskCreate` dependency graphs — none of which exist here. This version uses only the real `Agent` tool: three reviewers run in parallel as one-shot sub-agents, and the orchestrator does the integration itself instead of spawning a fourth "integrator" agent.

## Inputs
- `diff_path` or PR diff text
- list of changed files
- optional: review criteria, forbidden change areas, release risk level

## Outputs
- `_workspace/pr-review/static.md`
- `_workspace/pr-review/security.md`
- `_workspace/pr-review/tests.md`
- `_workspace/pr-review/final-review.md`

## Phase 0. Preconditions
1. Read the changed file list / diff and confirm review scope.
2. Ensure `_workspace/pr-review/` exists (create it if missing).
3. If the diff is empty or 0 files changed, report the reason and stop.
4. If more than 40 files changed, split into risk-ranked batches and review only the highest-risk batch this run.

## Phase 1. Parallel review
Spawn three `Agent` calls **in a single message** (parallel, `run_in_background: false` — integration needs all three results before continuing):

| Agent | Focus | Output file |
|---|---|---|
| static-reviewer | bugs, performance, style | `_workspace/pr-review/static.md` |
| security-reviewer | input validation, permissions, secret exposure | `_workspace/pr-review/security.md` |
| test-reviewer | test coverage mapping, missing regression tests | `_workspace/pr-review/tests.md` |

Each agent's prompt must include:
- the exact diff/file scope for this run
- explicit instruction: report only, never edit code
- the output file path to write findings to
- required finding format: severity (Critical/High/Medium/Low), file, line, one-sentence claim, supporting evidence

There is no cross-agent messaging — sub-agents cannot message each other directly. If a reviewer's findings raise a question for another domain (e.g. static reviewer spots a data-shape change that needs test-impact review), it notes that as a flagged item in its own report; you resolve it during Phase 2 by reading across reports, or by re-dispatching a follow-up agent if the ambiguity is load-bearing.

## Phase 2. Integration (done directly by you, not a sub-agent)
After all three reviewers return:
1. Read the three report files.
2. Order Critical/High findings first.
3. Merge duplicate issues that share a root cause.
4. Drop unsupported claims (no cited evidence).
5. Downgrade "test coverage only" gaps to "should-fix"; keep confirmed bugs as "must-fix".
6. Write `_workspace/pr-review/final-review.md` with exactly three sections: `must-fix`, `should-fix`, `watch`.

## Failure handling
- One reviewer fails: retry that role once.
- Same role fails twice: note the missing report in `final-review.md` and continue with the rest.
- Two or more reviewers fail: stop and report the failure to the user — there's no team object to tear down, just don't write a final report you don't trust.

## Final response format
Report to the user only:
1. must-fix count and file locations
2. should-fix count
3. path to the full report: `_workspace/pr-review/final-review.md`
