# AeroNews Newsfeed

Status: in progress · Updated: 2026-09-22

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

- Nothing active. Session closed with both open items captured as drafts in the
  plans system.

### Next

- Decide whether to fix placeholder headlines now or defer it. The ticker shows a
  literal placeholder when a feed item arrives without a title. A fix is drafted
  but not applied, because it touches the public pipeline, which is designated
  frozen. Waiting on the owner's decision.
- Decide whether the archive's intake step should keep untitled items. It
  currently drops them, so the archive silently loses them.
- Cross-referencing news items: linking related stories to each other and to the
  US counterpart of foreign regulatory news. Captured as a draft. Not urgent.

### Done

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

## Open questions for Claude

- What does "frozen" mean for the public pipeline when the designated-frozen file
  has changed six times in ninety days? A written test for when a change may go
  in would settle this better than case-by-case exceptions.
- The placeholder-headline case was seen once. Is it worth a fix before its
  frequency is measured?

## Sessions

Newest first. Roll entries older than the most recent three into
`archive/sessions/`.

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
