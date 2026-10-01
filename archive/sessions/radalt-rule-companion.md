# Radio Altimeter Rule Companion · archived sessions

Older entries rolled out of `projects/radalt-rule-companion.md`, newest first.

### 2026-09-08 (second session) · Claude Code

Did: Closed the duplicated-citation-data question from the previous session. The
source-of-truth file and the copy embedded in the deliverable are now compared on
every checker run; a mismatch fails loudly and names each differing field, and a
repair flag rewrites the copy from source. Verified by injecting drift, confirming
the failure, confirming the repair, and confirming the repair cannot push bad
citation data past the independent source checks. Deleted the retired generator
after recording the one thing in it that nothing else captured. Made end-of-session
state updates a standing rule across projects rather than a per-project habit.

Learned: The duplication is structural, not accidental — an offline deliverable
that must open from a local file cannot fetch its own data, so a copy has to be
embedded. The question was never how to remove the copy but how to stop trusting
it. Also worth noting the repair flag deliberately does not suppress the citation
checks; a sync tool that could silence the verifier would be worse than the drift
it fixes.

Left off at: Clean. Checker passes 90 claims, 0 failures, including the new
source-of-truth check. Generator deleted, backup retained. Next open item is
whether the memo generator deserves a real render test.

### 2026-09-08 (first session) · Claude Code

Did: Reworked the generated memo after a review found it asserting things the
rule does not support and omitting requirements that apply to the reader. Removed
an eligibility verdict and replaced it with what the rule actually states; added a
cost caveat for non-commercial operators, post-deadline operating restrictions, an
exemption requirement for night-vision-goggle operations, and a qualification that
post-deadline authorizations are case-by-case and not expected to become routine.
Added a scope statement at the top of the page, in the page footer, and at the top
of the memo, plus a staleness note in the memo footer. Excluded the page from
search indexes. Numbered the citations in copied text and keyed them to a sources
list so each claim is individually checkable. Redefined the citation rule, audited
all 90 claims against it, and corrected six. Retired the generator script behind a
guard that exits non-zero, and updated the project README to match.

Learned: Three things worth carrying forward. First, the rule's own text was
already sufficient for every correction — no new source research was needed, only
better selection from claims that already existed. Second, page attribution cannot
be done by document position: the source HTML is not in reading order, a late
section sits physically past the final page marker, and the last page carries no
marker at all. Per-paragraph metadata plus in-paragraph break markers is the only
reliable method. Third, an instruction can be wrong in a way that is only visible
once applied — collapsing straddling citations to a single page was requested,
implemented, and then correctly reverted because it produced labels pointing at
pages where the quoted sentence is not printed.

Left off at: Clean. Verifier passes 90 claims, 0 failures. An independent audit
of quoted-sentence page attribution reports 0 mismatches. The deliverable and its
deployment copy are identical, and the claims file agrees with the copy embedded
in the page on every field. The generator refuses to run. Next session should pick
up the duplicated-citation-data question in Open questions above.
