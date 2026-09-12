# pai-groundcontrol — Claude Operating Guide

Coordination notes and project state. No data, no application code. Read
`PUBLICATION-RULES.md` before writing a line — **this repository is public**,
and that applies to this file too.

## INVARIANTS

Constraints that hold regardless of what a task appears to ask for. If a change
would violate one, stop and raise it rather than proceeding.

### `main` is deliberately unfenced. Do not add a `pull_request` rule.

Ruleset **22656989** governs `main`. It carries `deletion` and
`non_fast_forward` and **must not carry `pull_request`**.

**Why.** State files here are pushed several times during a working session —
that is the entire workflow this repo exists to support. A pull-request step on
each of those pushes adds enough friction to kill the habit. A coordination repo
that is unpleasant to update stops being updated, and a stale coordination repo
is worse than no coordination repo. The value here is that the notes are
current, and direct push is what keeps them current.

**This is not an oversight.** It was decided on 2026-09-03, when the repo was
set up, and reaffirmed on 2026-09-12. The two rules that remain are the ones
that cost the workflow nothing: nobody needs to delete this branch or rewrite
its history.

**What happened when it was fenced.** A `pull_request` rule with an empty bypass
list was applied on 2026-09-09 during an org-wide protection pass. Every direct
push was rejected for the following nine days. Nothing surfaced it — the repo
simply stopped receiving updates, and the gap was only found while auditing
guardrail state for an unrelated reason. The rule was removed on 2026-09-12.

**The ruleset name is wrong.** It still reads `main: require pull request`,
which is now inaccurate and is the single most likely cause of this recurring.
A future sweep that reads the name and assumes the rule matches it will
"restore" a fence that was deliberately removed. Trust the rule list, not the
name. Renaming the ruleset is an open task.

**Before changing branch protection here**, derive the current state rather than
reading the name:

```
gh api repos/PAIConsulting/pai-groundcontrol/rulesets/22656989 --jq '[.rules[].type]'
```

Expected: `["deletion","non_fast_forward"]`. If `pull_request` appears, it was
added in error — remove it and note it in the project state file.

### An unfenced branch with a rationale is not a finding

Not every unprotected branch is a lapse. Some are load-bearing. Before applying
protection anywhere in a sweep, check whether the repo records a reason for the
gap. Applying a uniform fence across repos is not automatically safe: the pass
that broke this repo was correct for most of the repos it touched, and the cost
of the exceptions was paid silently by workflows that stopped working with no
error anyone read.

## Writing here

- One file per project under `projects/`, listed in `INDEX.md`.
- Update **Board**, append to **Decisions**, add a **Sessions** entry at the end
  of a working session, then update the project's row in `INDEX.md`.
- **Decisions are append-only.** Never edit or delete a past entry; supersede it
  with a new one that says what changed and why.
- Roll session entries older than the most recent three into
  `archive/sessions/`.
- Push directly to `main` — see the invariant above.
