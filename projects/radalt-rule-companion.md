# Radio Altimeter Rule Companion

Status: in progress · Updated: 2026-10-01

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
- [x] Citation data has one source of truth, with the derived copy verified automatically
- [ ] Memo rendering covered by something better than a hand-run harness
- [ ] Each of the 90 claims reviewed by a person, with a recorded verdict

## Board

### In progress

- Rebrand complete on a branch, not yet deployed. Waiting on a person-by-person
  review of the 90 claims before any publication decision.

### Next

- Human review of all 90 claims, each with a recorded verdict
- Decide the public address and whether search engines may index the page
- Decide whether the memo title should keep the word "compliance"
- Regenerate the sample memo so it matches the current page
- Consider a lightweight render test for the memo generator

### Done

- 2026-10-01 · Claim review tool's source links restricted to the official Federal Register site over https
- 2026-10-01 · Claim review tool added to the repository and documented in the README
- 2026-10-01 · Both branches pushed to a private repository under the company organization
- 2026-10-01 · Dated backup files untracked and ignored going forward; copies kept on disk
- 2026-10-01 · Project placed under version control with a baseline matching the live page
- 2026-10-01 · Page rebranded to the publishing organization: name, logo, colors, status marking
- 2026-10-01 · Wording that tied the page to another organization's document removed
- 2026-10-01 · Footer now names the publisher and states the page is not an FAA publication
- 2026-10-01 · Before-and-after proof that no claim, quote, page label or link changed
- 2026-10-01 · Claim counts reconciled: 90 machine-checked claims, none yet reviewed by a person
- 2026-09-08 · Rebate section rewritten to report the program, not a verdict on the reader
- 2026-09-08 · Non-commercial unit cost caveat added for the operator classes it applies to
- 2026-09-08 · Post-deadline restrictions and the night-vision-goggle exemption added
- 2026-09-08 · Authorization qualified as case-by-case and not routine
- 2026-09-08 · Staleness note added to the memo footer, in print and copied text
- 2026-09-08 · Scope statement added at page top, page footer, and top of the memo
- 2026-09-08 · Search engines excluded via robots meta and robots.txt
- 2026-09-08 · Citations in copied text numbered and keyed to a sources list
- 2026-09-08 · Citation rule redefined; all 90 claims audited against it
- 2026-09-08 · Generator script retired behind a guard, then deleted
- 2026-09-08 · Derived citation copy verified by the checker, with a repair flag
- 2026-09-08 · End-of-session state updates made a standing rule across projects

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

- 2026-09-08 · The claims file is the single source of truth; the copy embedded
  in the deliverable is a derived artifact, rewritten by tool and verified on
  every run. Why: extracting at load time was ruled out — the deliverable must
  open from a local file, where a browser cannot fetch a sibling JSON file. That
  makes the duplication structural, so it is checked rather than trusted. The
  checker now fails and names every differing field, and a repair flag rewrites
  the copy. The repair path cannot launder bad citation data: the source checks
  run against the rule text regardless.

- 2026-09-08 · A documented manual procedure was rejected as the fix. Why: the
  drift that motivated this happened while such a procedure was in place. A
  procedure that depends on remembering is not a control.

- 2026-09-08 · The retired generator was deleted rather than kept behind its
  guard. Why: a file whose only behaviour is to refuse to run is a trap for a
  session that skims the guard and assumes it is the build path. What was worth
  keeping — chiefly how the embedded logo data URI was produced, which nothing
  else records — is now in the project README. The last version is retained as
  a dated backup outside the working set.

- 2026-10-01 · The 90 claims are described as machine-checked, not as verified by
  a person. Why: An earlier human review covered 37 claims in a different
  document; the 90 claims here have been machine-checked only, and a human
  review is in progress. The automated checker proves each quote is verbatim and
  each page number is right; it does not judge whether the plain-language
  restatement is fair. Publication waits on that human pass.

- 2026-10-01 · A rebrand is proven safe by hashing, not by reading the diff. Why:
  the page holds 123 rendered claim blocks in very long lines, where a stray edit
  is easy to miss by eye. The ordered list of every rendered claim (text, page
  label, links, quote), the embedded claims block and the claims file were hashed
  before and after and must be identical, alongside the existing checker.

- 2026-10-01 · System fonts were kept instead of the brand typeface. Why: loading
  a web font from a third party would send each reader's address to that party,
  and the page promises that nothing leaves it. The promise outranks the typeface.

- 2026-10-01 · The accent color is used only as a rule under the header band, and
  error text has its own color outside the brand palette. Why: the accent is too
  light on white to meet contrast minimums for text or a focus ring, and an error
  message in the same navy as everything else does not read as an error.

- 2026-10-01 · The disclaimer names only the FAA. Why: naming other organizations
  in a statement of non-affiliation creates the association it is meant to remove.

- 2026-10-01 · The deployment copy was left untouched and the search-engine
  exclusion kept. Why: both are publication decisions that follow the human
  review, and the live page should not change until then.

- 2026-10-01 · Backup files were untracked with a new commit rather than removed
  from earlier commits. Why: the instruction was to leave history as it is, and
  the repository is private. The ignore rule keeps new safety copies local; the
  two earliest commits still contain the old ones, and that is accepted. Before
  this repository's visibility ever changes, its history needs a separate review,
  because the baseline commit records the page as it stood before the rebrand.

- 2026-10-01 · This entry replaces the wording of the earlier 2026-10-01 entry
  about machine-checked claims; that entry is left as written. The 90 claims are
  machine-checked, not human-verified. The earlier 37-claim human review belonged
  to a different document. Whether any of those 37 overlap the 90 has not been
  checked. Human review of the 90 is in progress using the claim review tool.
  Publication waits on that pass.

- 2026-10-01 · Correction to the entry above. The earlier 2026-10-01 entry about
  machine-checked claims was in fact edited in place, through a merged pull
  request that landed after the entry above was written, so the statement that
  it was left as written is not accurate. Both entries now agree: the 90 claims
  are machine-checked only, the earlier 37-claim human review belonged to a
  different document, and publication waits on human review of the 90. Whether
  any of the 37 overlap the 90 has not been checked.

## Open questions for Claude

- Is a render test worth building for the memo generator, given verification is
  currently a hand-run harness that stubs the DOM?
- What is the lightest way to record a person's verdict per claim so that it
  travels with the claims file and the checker can report review coverage?

## Sessions

Newest first. Roll entries older than the most recent three into
`archive/sessions/`.

### 2026-10-01 (second session) · Claude Code

Did: Gave the project a private remote under the company organization and pushed
both branches. A pre-push check found the ignore file covered only one of sixteen
dated backup files; the other fifteen were already committed. With history left
untouched by instruction, they were untracked in a new commit and a pattern added
so future safety copies stay local. Confirmed afterwards that the repository is
private, both branches arrived at the expected commits, and every backup is still
on disk.

Learned: An ignore rule only governs files that are not yet tracked, so "is it in
the ignore file" and "is it out of the repository" are different questions and
need checking separately. Also, with backups tracked on one branch and untracked
on the other, switching between the two removes them from disk on the way back;
merging the newer branch into the older one ends that.

Later the same session: committed the claim review tool and a README line on how
to use it. An automated review of that commit found the tool built its source link
from the loaded file without checking the address; the link now accepts only an
https address on the official Federal Register site and otherwise falls back to
the built-in one. Recorded a superseding decision on how the claim counts are
described.

Left off at: Remote in place, branches in sync, working folder clean. Human review
of the 90 claims is in progress with the review tool; publication decisions wait
on it.

### 2026-10-01 (first session) · Claude Code

Did: Inventoried the project ahead of publication, then rebranded the page.
Found the folder was not under version control and fixed that with a baseline
commit that matches the live page byte for byte. Reconciled two claim counts that
had been confused: the page carries 90 claims, all passing the automated checker,
while a 37-claim human review belonged to a different document. Replaced the
masthead name and logo, moved the colors to the publisher's brand guide, reworded
the status marking, removed a sentence tying the page to another document, and
added a footer line naming the publisher and stating the page is not an FAA
publication. Gave the memo form's error text its own readable color.

Learned: The page's small number of identity elements made the rebrand cheap; the
expensive part was proving nothing else moved. Hashing the rendered claims in
order turned that into a yes-or-no answer. Also, "verified" had been carrying two
meanings — machine-checked against the source, and reviewed by a person — and
only the first is true of this page today.

Left off at: Rebrand committed on a branch; checker passes 90 claims, 0 failures,
0 warnings, identical to before. Not deployed, and the deployment copy still
matches the live page. The sample memo file still shows the old look. Next is the
human review of the 90 claims, then the publication decisions listed under Next.

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
