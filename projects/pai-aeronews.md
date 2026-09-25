# AeroNews Newsfeed

Status: in progress · Updated: 2026-09-25

## Brief

An automated aviation news ticker. Every hour it collects articles from public RSS
feeds, writes a one-sentence takeaway for each with a small language model, and
publishes a scrolling set of cards for embedding in a web page. The same ingestion
pipeline also feeds a research archive and several internal analysis agents, which
are tracked separately.

Done, for the current phase, looks like a ticker where every card has a real
headline, and a clear decision on whether to get more analytical value out of the
stream than one card per article.

## Board

### In progress

- Restructure of the project's Claude Code instructions into a short always-loaded
  file plus path-scoped rule files, with roadmap items that existed only in the
  old file migrated into the roadmap. Open as a pull request, waiting on the
  owner's review.

### Next

- After the restructure merges, confirm in a fresh session that each rule file
  loads when its paths are touched, rather than assuming it does.
- Decide whether the archive's intake step should keep untitled items. It
  currently drops them, so the archive silently loses them.
- Cross-referencing news items: linking related stories to each other and to the
  US counterpart of foreign regulatory news. Captured as a draft. Not urgent.

### Done

- 2026-09-23 · Placeholder headlines fixed: a missing headline is now written in
  the same per-article model call as the takeaway, with no extra call
- 2026-09-22 · Seven permission allow rules that Claude Code flagged as unsafe
  were resolved: one narrowed to a safe form, six removed
- 2026-09-22 · Two malformed permission rules removed: one was not a runnable
  command, and the other was shown by testing never to match
- 2026-09-22 · A private plans repository set up, with its default branch
  deliberately left without a pull-request requirement
- 2026-09-22 · The headline fix and the cross-referencing idea captured as plan
  drafts rather than left as loose notes

## Decisions

Append-only. Never edit or delete a past entry; supersede it with a new one.

- 2026-09-22 · A permission rule whose wildcard came from a regex or shell-glob
  character is removed, not rewritten as a broad wildcard. Why: those rules were
  saved one-off approvals for a single command. Rewriting them with the wildcard
  at the end would have approved whole command families, including some that can
  write files or run other programs. Removing them costs one prompt the next time
  such a command runs.

- 2026-09-22 · Tool behaviour is checked by testing it, not by reading the rule
  text. Why: one rule looked broad on paper but never matched anything when
  tested, and the list of flagged rules came from the tool's own startup warnings
  rather than from pattern-matching the file. Both corrected what reading the
  file suggested.

- 2026-09-22 · The plans repository's default branch blocks deletion and
  force-push only, with no pull-request requirement, the same arrangement as this
  repository and for the same reason. Why: plans are captured several times a
  session, and friction on each capture kills the habit. The rule list, not the
  ruleset's name, is the record of what it enforces.

- 2026-09-22 · Ideas and pending decisions are filed as plan drafts, not as
  untracked notes in the product repository. Why: a loose file in a working tree
  is easy to lose or commit by accident, and a draft carries a snapshot of related
  work and an explicit "waiting on" state.

- 2026-09-25 · The project's Claude Code instructions are split: universal rules
  stay in the file every session loads, and area-specific detail moves to rule
  files that load only when matching paths are touched. Dated measurements and
  incident history move to a separate decisions document. Why: the single file
  had grown past twelve hundred lines, most of it relevant only to one area, and
  all of it was paid for in every session. A restructure is checked line by line
  for what it drops before it lands; this one would otherwise have lost a merge
  checklist, the renderer rules, and nineteen roadmap items, and would have
  confined a security rule to a directory where it would rarely load.

- 2026-09-25 · The rule files are tracked in git, with the rest of the local
  Claude Code directory still ignored. Why: rules that live only on one machine
  are invisible to every other clone and to any other session reading the
  repository, and the always-loaded file now points at them.

## Open questions for Claude

- What does "frozen" mean for the public pipeline when the designated-frozen file
  has changed six times in ninety days? A written test for when a change may go
  in would settle this better than case-by-case exceptions.
- Now that the placeholder-headline case is fixed, how often does it actually
  occur? Is it worth instrumenting and measuring going forward?

## Sessions

Newest first. Roll entries older than the most recent three into
`archive/sessions/`.

### 2026-09-25 · Claude Code

Did: Reviewed a restructure of the project's Claude Code instructions from one
large file into a short root file plus seven path-scoped rule files and two
on-demand documents, and opened it as a pull request. Checked every removed line
against the new files before anything moved. The owner chose five fixes from
what that found: two merge-checklist steps and a security rule restored to the
root file, the card-renderer rules restored to their rule file, a contact rule
widened to cover skill files, and nineteen roadmap items migrated into the
roadmap. An old version changelog was left out. While branching, found that a
change merged after the restructure was drafted had edited the old file; ported
it so the restructure would not undo it.

Learned: Two things would have gone wrong without a check. First, the new rule
files were ignored by git twice over — once by the repository's own ignore file
and once by a machine-wide one — so the pull request would have shipped a short
root file pointing at rules that existed only locally. Second, a restructure
drafted against an older copy of a file silently reverts whatever merged since.
Compare against the current main branch, not the copy the draft was made from.

Left off at: Pull request open with twelve files, waiting on the owner's review.

### 2026-09-22 · Claude Code

Did: Cleaned up this project's local permission rules. Claude Code's own startup
warnings flagged seven allow rules with a wildcard in the middle; one became a
narrow trailing-wildcard rule and six were removed. Two more malformed rules were
removed: one was a fragment that could never be a runnable command, and the other,
which looked broad, matched nothing in headless tests. Then
investigated a ticker card that showed a placeholder instead of a headline. It
traced to a hard-coded fallback in the ingestion step, with a second effect: the
archive intake drops the same items. A fix was drafted, reusing the existing
per-article model call rather than adding one, but not applied because the file
is designated frozen. Finally, set up the plans system and filed two drafts: the
pending headline decision, and an idea for cross-referencing news items.

Learned: Reading a permission rule is not the same as knowing what it matches.
One rule looked broad and matched nothing, and the reliable list of flagged rules
came from the tool itself. Separately, a cache that makes repeat work free can
also keep a bad result on screen. The drafted fix needed a cache change, or the
already-cached card would have kept its placeholder for as long as the cache
entry lived.

Left off at: Both drafts filed, the headline decision waiting on the owner, and
the local permission file checked clean.
