# AeroNews Newsfeed · archived sessions

Older entries rolled out of `projects/pai-aeronews.md`, newest first.

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
