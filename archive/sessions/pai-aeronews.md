# AeroNews Newsfeed · archived sessions

Older entries rolled out of `projects/pai-aeronews.md`, newest first.

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

### 2026-09-26 · Claude Code

Did: Audited the Claude Code instruction files that load for this project, plus
the owner's global ones, against the current model and against the repository
itself. Most findings were stale facts and files contradicting each other, not
old prompting style. Applied the project-side fixes as one pull request, which
the owner merged, and a small commit to the global files. Filed a plan draft
for the brand-colour disagreement and added line-level detail to an existing
draft for cleaning up dead tool references.

Learned: The most useful check was comparing each claim in a rule file with the
tree: counts, line numbers and secret lists had drifted, and one checklist item
referred to a feature that had been switched off. Also, a file that git ignores
cannot ride along in a pull request, so an edit to it stays local until someone
decides to track it.

Left off at: Merged. The fresh-session check that rule files load is still open.

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
