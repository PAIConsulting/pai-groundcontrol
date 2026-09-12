# Documentation Drift and Repo Guardrails

Status: in progress · Updated: 2026-09-12

## Brief

Two related strands of upkeep across the internal tooling repos. The first is
documentation drift: canonical notes that were accurate when written and became
wrong when the system moved, with nothing watching for the transition. The
second is the guardrail layer itself — which branches are fenced, which are
deliberately not, and whether either fact is recorded anywhere a future session
will look.

The two strands met this session. A nightly review agent had been reporting the
same drift items for up to nineteen consecutive nights, including a document
that contradicted itself about branch protection. Reconciling that contradiction
required an audit of the actual guardrail state, and the audit found a fence
that had been applied to a repo whose design depends on not having one.

Done looks like: no canonical document asserting live system state it cannot
verify, and every deliberate gap in the guardrail layer recorded as deliberate,
in the repo it applies to.

## Board

### In progress

- Nothing active. Session closed with all three review branches open and the
  guardrail constraint recorded.

### Next

- Redesign the two direct-push bot writers so their repos can be fenced without
  breaking them, or accept the gap permanently and say so
- Decide whether the recurring-drift list deserves a standing review rather than
  a nightly re-report

### Done

- 2026-09-12 · Six drift items corrected in the knowledge base, three in other
  repos, across three review branches
- 2026-09-12 · Guardrail state audited across seven repos and recorded as a
  dated, derived table rather than an assertion
- 2026-09-12 · A self-contradicting document reconciled after eight nights of
  being reported
- 2026-09-12 · Deliberate unfenced branches distinguished from lapsed ones in
  the audit record
- 2026-09-12 · This repo's own fence removed after it was found blocking the
  workflow the repo exists to support

## Decisions

Append-only. Never edit or delete a past entry; supersede it with a new one.

- 2026-09-12 · This repo's default branch is deliberately unfenced and stays
  that way. Why: state files are pushed several times per working session, and
  a pull-request step on each one adds enough friction to kill the habit the
  repo exists to create. A coordination repo that is unpleasant to update stops
  being updated, and a stale coordination repo is worse than none. The
  protections that do not impede the workflow — no branch deletion, no
  force-push — are kept. This supersedes the fence applied on 2026-09-09,
  which was applied without reference to that constraint.

- 2026-09-12 · An unfenced branch with a written rationale is treated as a
  different class of object from an unfenced branch nobody noticed, and the
  audit record must distinguish them. Why: the natural remedy for the second —
  apply the fence — is precisely the wrong action for the first. An audit that
  cannot tell them apart will break working pipelines while believing it is
  closing a finding.

- 2026-09-12 · Guardrail state is recorded as a dated table derived from the
  platform API, never as a prose assertion. Why: the same claim had gone stale
  three times in three weeks, and one of the corrections was itself wrong on a
  point of fact within the same session it was written. A dated derivation is
  checkable; a present-tense assertion rots silently.

- 2026-09-12 · Dated records keep their original wording when a finding they
  describe is later corrected; only live documents are rewritten. Why: a dated
  entry is evidence of what was believed on that date, which has value a
  silently-corrected entry destroys. Corrections are attached inline, and the
  live documents that assert the claim in the present tense are the ones fixed.

## Open questions for Claude

- The two remaining unfenced branches both fail for the same reason — a bot
  writer that pushes directly. Is a bypass actor the right fix, or should the
  writers open pull requests like everything else? The second is more work and
  more correct; the first is available today.
- Is a nightly re-report of the same unfixed item the right pressure, or does it
  train the reader to skim? Some items ran nineteen nights before being fixed.

## Sessions

Newest first. Roll entries older than the most recent three into
`archive/sessions/`.

### 2026-09-12 · Claude Code

Did: Cleared a backlog of documentation drift that a nightly review agent had
been reporting for between eight and nineteen consecutive nights. Nine items
across three repos, landed as three review branches — one per repo, since the
changes shared a cause but not a review audience. The items were of three kinds:
completed work still listed as an active blocker; a corrected research finding
whose pre-correction wording survived in two live documents and, more seriously,
in a methods note that taught the reversed version as its worked example; and a
concept note describing an agent's trigger and its enabling precondition as they
were designed rather than as they were built.

Reconciling a document that contradicted itself about branch protection required
auditing the actual state, which turned up two things. Ruleset identifiers are
scoped to a repository, so an earlier correction asserting that an identifier
"does not resolve" was itself wrong — it resolves, in the repo that owns it.
And this repo's own default branch had been fenced three days earlier, silently
rejecting every direct push for nine days. The fence was removed this session
and the workflow verified by pushing this file.

Learned: The failure mode is not that documents go stale — it is that nothing
watches for the moment they do. Every item here was accurate when written. The
second-order version showed up too: a correction note that asserted live state
went stale in the same session it was authored, which is the argument for
recording a derivation command instead of a value.

Also worth carrying forward: a guardrail applied uniformly is not obviously
safe. The fence that broke this repo was correct for five of the seven it was
applied across. The cost of the two exceptions was paid silently, by a workflow
that simply stopped working, for nine days, with no error anyone read.

Left off at: Three review branches open and awaiting merge. This repo's fence
removed and the push path confirmed working. The guardrail constraint is now
recorded in this repo so a future sweep meets it instead of rediscovering it.
