# AeroNews Newsfeed

Status: in progress · Updated: 2026-10-07

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

- Paper-metadata enrichment, first step: the academic intake keeps the
  researcher, institution, topic and reference metadata it already receives, in
  a separate file beside the paper store. Two pull requests wait on the owner's
  merge, and the workflow change must merge first.

### Next

- Paper-metadata enrichment, second step: backfill that metadata for the papers
  already in the store, and refresh the reference lists, which are often still
  empty when a paper is first ingested. Captured as a card in the product
  repository.
- The instruction that every session read the platform documents first was made
  conditional in this project. The same preamble likely sits in the other
  platform repositories and may need the same change.
- Confirm in a fresh session that each rule file loads when its paths are touched,
  rather than assuming it does. A check at the end of the 2026-09-26 session was
  inconclusive, because the rule file had already been read in that session.
- Decide the canonical navy and cyan for the company brand. Three files disagree
  and no code was changed. Captured as a plan draft.
- Decide whether the Act Now tool skill should be tracked in git. It is ignored
  today, so its edits are local only.
- Decide whether the archive's intake step should keep untitled items. It
  currently drops them, so the archive silently loses them.
- Cross-referencing news items: linking related stories to each other and to the
  US counterpart of foreign regulatory news. Captured as a draft. Not urgent.

### Done

- 2026-10-03 · Roadmap item for a dead dependency, left from the earlier
  migration to Anthropic models, checked off after confirming the package
  manifest and lockfile are both free of it
- 2026-10-03 · Roadmap line about a retired calibration anchor corrected to match
  the skill file
- 2026-10-03 · Remaining audit fixes merged: ticker direction corrected in a
  frontend rule, the platform-reading preamble made conditional, an inline
  API-key example replaced, and a research skill's retired and dated notes
  removed
- 2026-10-03 · Single quotes are now escaped in two internal review pages, so a
  value can no longer break out of a single-quoted attribute
- 2026-09-26 · Audit fixes to the project's instructions merged: stale counts,
  line numbers and a disabled-digest checklist item corrected, a missing secret
  added to the list, the branch-naming rule matched to practice, and an
  unsourced cost total removed
- 2026-09-25 · Restructure of the project's Claude Code instructions merged, with
  roadmap items from the old file migrated into the roadmap
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

- 2026-09-26 · Rule files state facts as commands or symbol names, not as counts
  or line numbers. Why: an audit found the job count, the store count and three
  script line references all stale within a day of the restructure. A written
  number cannot be re-checked by the next reader; a command can.

- 2026-09-26 · A wrong claim in a rule is rewritten so the file reads correctly,
  with no dated migration wording left in it. Why: phrases like "now" and "as
  before" describe a version the reader never saw.

- 2026-10-03 · A retired rule or calibration case is deleted from the instruction
  file, not kept struck through with an explanation. Dated "currently" notes are
  rewritten as standing conditions. Why: a model reads struck-through text and
  dated snapshots as live instructions, and the history already lives in version
  control.

- 2026-10-03 · A roadmap item for removing a dependency is checked off only after
  the package manifest and the lockfile are both confirmed free of it. Why: the
  item outlived the migration that made it obsolete, because nobody re-checked
  the files. An item closed from memory can just as easily be closed while the
  dependency is still there.

- 2026-10-07 · Paper metadata is stored in a separate, compact file keyed by
  paper id, not inside the paper store. Why: measured on a live run, it would
  have more than tripled the size of each stored paper. At the store's cap that
  passes the hosting platform's hard per-file push limit, and the tagging agent
  reads the whole store on every run. The separate file is pruned to the
  store's papers, so it shares the store's cap, and a size test guards it.

- 2026-10-07 · A citation count is not stored at intake. Why: it was zero on
  every paper sampled, because papers are days old when they arrive. A zero
  stored once and never refreshed would later read as "never cited." If it is
  wanted, it belongs in a refreshable backfill with its own fetch date.

## Open questions for Claude

- What does "frozen" mean for the public pipeline when the designated-frozen file
  has changed six times in ninety days? A written test for when a change may go
  in would settle this better than case-by-case exceptions.
- Now that the placeholder-headline case is fixed, how often does it actually
  occur? Is it worth instrumenting and measuring going forward?

## Sessions

Newest first. Roll entries older than the most recent three into
`archive/sessions/`.

### 2026-10-07 · Claude Code (paper metadata, step one)

Did: Checked a sample of recent papers to see which metadata fields actually
arrive populated, then measured how much storing them would grow the paper
store. Storing them in the store would have crossed the hosting platform's
per-file limit at the store's cap, so the owner chose a separate file. Opened
two pull requests: a small workflow change that carries the new file, and the
intake change itself, with tests, a size guard, documentation updates, and a
card for the backfill step.

Learned: Checking before building paid off twice. The planned field list
assumed every field was useful at intake, but one was always zero and another
was often empty, and the size check found a limit the plan had not anticipated.
The size guard was also made to fail on purpose before it was trusted.

Left off at: Both pull requests await the owner's merge, workflow change first.

### 2026-10-03 · Claude Code (Anthropic-only cleanup)

Did: Part of a cleanup across the owner's work folders after a scan for
non-Anthropic AI services. For this project the only finding was a roadmap
item for a dependency left over from the earlier move to Anthropic models.
Confirmed the dependency is absent from the package manifest and lockfile,
checked the item off, bumped the roadmap version, and opened one pull request.
No code changed.

Learned: The roadmap had carried a finished item as open since the migration.
Checking it took one search of the two package files.

Left off at: Merged. Nothing open in the product repository.

### 2026-10-03 · Claude Code

Did: Applied the remaining findings from the 2026-09-26 instruction audit. A
frontend rule had the ticker direction backwards and was corrected after the
code was checked. The platform-reading preamble now applies only to
platform-level work. An inline API-key example was replaced with a pointer to
the approved hidden-prompt method. A research skill's retired anchor and dated
notes were removed, in both of its copies. Two internal pages now escape single
quotes. Built the project, loaded both pages in a headless browser, ran the test
suite, and opened one pull request. Edits to the ignored Act Now skill stayed
local.

Learned: A drift guard is only trusted after it has been made to fire. The two
skill copies were confirmed identical, then one was changed on purpose to see
the warning, then restored. Also, the browser automation server could not start
without a full Chrome install, but a headless browser already on the machine
was enough to load the pages.

Left off at: Both pull requests merged. Nothing open in the product repository.
