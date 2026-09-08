# Radio Altimeter Rule Companion

Status: in progress · Updated: 2026-09-08

## Brief

A single-file, offline reading aid for a published FAA final rule
(*Requirements for Interference-Tolerant Radio Altimeter Systems*, 91 FR 48656,
July 31, 2026, Docket FAA-2025-5666). The page restates the rule in plain
language and ties every statement to the printed Federal Register page it came
from, with a link that opens the FAA's own paragraph. A four-question flow
generates a one-page compliance memo — deadline, near-term action, estimated
cost, the rebate program, and what post-deadline operation costs you — that can
be printed or copied as text. It ships as static files with no server, no
analytics, no cookies, and no storage; nothing a reader enters leaves the page.

Done looks like: every sentence on the page traceable to a page number a reader
can check, no assertion the rule does not support, and no silent staleness.

## Definition of done

- [x] Every claim carries a verbatim quote and a printed page number
- [x] Automated check that quotes and page numbers match the source
- [x] Memo reports what the rule states rather than adjudicating the reader's position
- [x] Scope statement visible on page, in print, and in copied text
- [x] Staleness disclosed in the memo, not only on the page
- [x] Kept out of search indexes
- [ ] Citation data has one source of truth rather than two hand-synced copies
- [ ] Memo rendering covered by something better than a hand-run harness

## Board

### In progress

- Nothing active. Session closed at a clean state.

### Next

- Decide whether to collapse the two copies of the citation data into one
- Add a sync check comparing the claims file against the copy embedded in the page
- Consider a lightweight render test for the memo generator

### Done

- 2026-09-08 · Rebate section rewritten to report the program, not a verdict on the reader
- 2026-09-08 · Non-commercial unit cost caveat added for the operator classes it applies to
- 2026-09-08 · Post-deadline restrictions and the night-vision-goggle exemption added
- 2026-09-08 · Authorization qualified as case-by-case and not routine
- 2026-09-08 · Staleness note added to the memo footer, in print and copied text
- 2026-09-08 · Scope statement added at page top, page footer, and top of the memo
- 2026-09-08 · Search engines excluded via robots meta and robots.txt
- 2026-09-08 · Citations in copied text numbered and keyed to a sources list
- 2026-09-08 · Citation rule redefined; all 90 claims audited against it
- 2026-09-08 · Generator script retired behind a guard

## Decisions

Append-only. Never edit or delete a past entry; supersede it with a new one.

- 2026-09-08 · The memo reports what the rule says and does not decide the
  reader's status. Why: the four questions a reader answers cannot establish
  eligibility for a rebate program administered by a different agency under a
  different order. Printing a verdict implied a determination the page has no
  basis to make.

- 2026-09-08 · A page citation names the printed page where the **quoted
  sentence** appears, not the page where its paragraph begins. Why: a reader is
  locating a sentence, not a paragraph. A paragraph anchor frequently begins on
  the previous page, so anchoring the label to the paragraph sends readers to a
  page where the sentence is not printed.

- 2026-09-08 · When a quoted sentence crosses a page break, the citation is
  written as a range and rendered "pp." Why: some sentences genuinely straddle
  — one breaks mid-phrase at "engaging hover / autopilot modes". Neither single
  page is correct on its own. Three of 90 claims are ranges.

- 2026-09-08 · Two claims sharing one paragraph anchor may legitimately carry
  different page labels. Why: this reads as an inconsistency but is correct when
  the two quoted sentences fall on either side of a break. The sources list now
  states this so a reader does not mistake it for an error. This supersedes an
  earlier decision the same day to collapse such labels to a single page, which
  was wrong and was reverted.

- 2026-09-08 · The generator script is retired rather than repaired. The
  deliverable is now maintained by hand and is its own source of truth. Why: the
  page had been hand-edited across several sessions and the generator no longer
  reproduced it. A generator that cannot regenerate its own output is a stale
  copy that happens to be executable. Backporting several sessions of divergence
  was judged not worth the cost when nothing exercises regeneration.

- 2026-09-08 · The citation pipeline is kept and stays canonical. Why: it is the
  machinery that makes every page number checkable, and it earned its keep this
  session — the verifier independently caught two mis-labeled citations that a
  separate audit had also flagged, from a different source document.

## Open questions for Claude

- The claims data now lives in two places: a standalone file the verifier reads,
  and a copy embedded in the deliverable that the page reads. These drifted once
  this session and silently reverted a set of page labels. Extract at load time,
  add a sync check, or accept the duplication with a documented procedure?
- Is a render test worth building for the memo generator, given verification is
  currently a hand-run harness that stubs the DOM?
- The retired generator is kept for reference behind a guard. Keep it, or delete
  it once its useful patterns are recorded?

## Sessions

Newest first. Roll entries older than the most recent three into
`archive/sessions/`.

### 2026-09-08 · Claude Code

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
