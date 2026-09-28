# Conference Hub

Status: in progress · Updated: 2026-09-28

## Brief

An offline-capable web app that turns a set of staff instruction documents into
one installable hub: a single home screen icon, many tools inside it, searchable,
working without a network. Staff read it on their own phones, often at the back
of a room with poor signal, so offline capability and a small-screen floor are
requirements rather than refinements.

A hard constraint shaped the whole architecture — the source documents may not be
shared with any AI. That turned the work from "convert these documents" into
"build a kit and fill it in yourself," which proved to be the better outcome
because it scales past the first few documents and can be handed to someone else.
The kit is three offline browser tools: a content builder that reads a document's
structure and writes a content file, an icon maker that produces the home screen
icon set, and a library indexer that makes documents searchable without converting
them at all. None of them upload anything or touch a network.

Done looks like: staff find the right instruction on their own phone, at the back
of a room, with no signal — and someone other than the author can add next year's
documents without help.

## Definition of done

- [x] Hub shell, renderer, and offline service worker
- [x] Offline content builder that reads document structure without uploading
- [x] Icon maker producing the full home screen icon set
- [x] Full-text search across converted tools
- [x] Library indexer making unconverted documents searchable
- [ ] Custom subdomain provisioned — blocks authenticated deployment
- [ ] Access gating configured per path rather than site-wide
- [ ] Remaining documents converted
- [ ] Hosting moved to a company-owned account rather than a personal one
- [ ] Real logo and app icons replacing the placeholders
- [ ] Outstanding content questions answered by the project owner

## Board

### In progress

- Session support workflow, part 1 of 2 (step-at-a-time walkthrough) — committed,
  waiting on a manual deploy and a phone check before part 2 starts
- Converting the next three documents, to find out what else the source format
  throws at the converter

### Next

- Session support workflow, part 2 of 2: the during-session panel (count and
  restart log, note-sent marks, leaving-the-room checklist, security card) and a
  per-session record kept on the phone
- Commit the library indexer work
- Send the outstanding questions list to the project owner
- Move the subdomain request forward — the only blocker nothing else routes around

### Blocked

- Authenticated deployment — waiting on a DNS record for a custom subdomain. The
  access product does not work on the hosting platform's default domain, so no
  amount of other progress reaches a gated deployment.
- Note-taking tool — waiting on a decision about where notes are stored. A
  content decision, not a coding problem.

### Done

- 2026-09-28 · Session support workflow walkthrough: setup, one step at a time
  with clock times from the session start, list view, solo mode, next session,
  end of day; steps kept in one editable data file; first automated test file
- 2026-09-12 · Library indexer shipped; hub search now covers unconverted documents
- 2026-09-12 · Search reads HTML as text rather than markup; phrase search added;
  result caps lifted and match counts reported
- 2026-09-11 · Collapsible sections, offline full-text search, automatic linking,
  rebuilt contact cards, and the icon maker
- 2026-09-11 · Hosting strategy settled; first document converted and committed
- 2026-09-09 · Hub shell built and tested; content builder and shape report
  established as the two-artifact content pipeline

## Decisions

Append-only. Never edit or delete a past entry; supersede it with a new one.

- 2026-09-09 · Source documents are never shared with any AI, and every tool in
  the kit runs entirely in the browser with no network and no upload. Why: the
  constraint was confirmed with the project owner and is absolute — not a
  restriction on one upload channel. Building offline tools satisfies it by
  construction rather than by discipline, so no future session can violate it by
  forgetting.

- 2026-09-09 · Build a kit, not a set of conversions. Why: converting documents
  by hand does not scale past the first few and cannot be handed off. A builder
  that someone else can run makes next year's update a task rather than a
  project.

- 2026-09-09 · A shape report — block types and counts only, no words — is what
  gets sent for rendering work. Why: rendering code can be written against a
  document's structure without the content ever moving, which keeps the no-AI
  constraint intact while still allowing help with the code.

- 2026-09-11 · The hub indexes; it does not replace. Credentials stay behind the
  existing sign-in, schedules stay in the existing event system, badge scanning
  stays with the colleague who owns it. Why: rebuilding any of them would produce
  a slower, less accurate duplicate with a second source of truth. The hub
  carries a tile that opens each.

- 2026-09-11 · A standalone installable app rather than a page on the existing
  website. Why: the hub installs to a home screen and runs offline, which needs a
  service worker at the root of its own scope. A page inside a larger site cannot
  provide that.

- 2026-09-12 · A document does not have to become a tool to be findable. Why:
  conversion is slow per document and produces something better; indexing is fast
  across all of them and produces something merely findable. Running both means
  search is useful from the first day rather than after the fifteenth conversion.

- 2026-09-12 · Gating stops being a preference and becomes a requirement once a
  search index ships. Why: a search index contains the full text of every document
  in it — one file, one download, everything. Those documents currently sit behind
  whatever access control their shared folder has, so an index on an open address
  would be strictly worse than what exists today. For demonstration purposes the
  index is run locally and never deployed.

- 2026-09-12 · Gate by path rather than site-wide. Why: the lowest-sensitivity
  content is used at the worst possible moment for a login — someone crouched
  behind equipment with one hand free — and it is not sensitive. Protecting a path
  keeps that open while putting the search index and everything else behind
  sign-in. This turns an all-or-nothing question into a design decision.

- 2026-09-12 · Do not fight the paper preference. Why: paper wins in a bag behind
  equipment — no battery, no login, works with dirty hands. The app is the copy
  you have when the bag is in another room, plus the thing that is searchable.
  Positioning it as a replacement would lose an argument that does not need to be
  had.

- 2026-09-28 · No AI session opens, reads or searches the hub's converted
  document files. A session may touch only the workflow steps file and the tool
  list. Links from the workflow into a converted document open it by its id, with
  no search terms. Why: the 2026-09-09 constraint covers the converted files as
  much as the originals. A session had read one to pick search words, and the
  rule was made explicit so it cannot recur through a well-meant shortcut.

- 2026-09-28 · The session support workflow's steps are data, seeded from the
  owner's own paraphrases, and unanswered policy points (count timing, who runs
  the Q&A tool, the recording rule) are data values or "pending" labels. Why:
  when answers arrive they become a one-file edit, not a rebuild, and no
  document wording enters the code.

- 2026-09-28 · Pushing to the main branch does not deploy the hub. It is a
  manual upload, done by the owner after each change is verified. Why: the
  hosting is a direct upload rather than connected to the repository, so a push
  is a record of the change, not a release.

## Open questions for Claude

- The first converted document is a reference document being used as an operating
  procedure, and is too much to hold at once on a phone. The recommendation is to
  split it into a short during-the-session checklist with the reference behind it
  — same content, two shapes. This is a content decision for the project owner;
  worth confirming it is still the highest-value thing to raise.
- Whether the running list of cross-document references collected during
  conversion is a handful of links or an actual web. Expected to become clear by
  the fourth document.

## Sessions

Newest first. Roll entries older than the most recent three into
`archive/sessions/`.

### 2026-09-28 · Claude Code

Did: Built part 1 of the session support workflow — a guide that walks the
person supporting a session through their shift one step at a time. Setup takes
the room, the scheduled start, which organization they are with, whether they
have a partner, and an optional session ID. Every step shows its clock time from
the start; the current step is highlighted, late steps turn amber, and nothing
alerts or advances on its own. Solo mode adds preparation steps and a "rules
pending" notice. Progress stays on the phone; nothing is sent. Added the hub's
first automated tests for the time rules and ran a phone-size browser check,
including a check that the page makes no outbound requests.

Learned: The no-AI rule needs stating for the converted files, not just the
originals — a session reached for one to pick search words, which was well meant
and still out of bounds. Also, open policy questions are best carried as data
("pending", a default number) so the build is never waiting on an answer.

Left off at: Part 1 committed and ready for the owner's manual deploy and phone
check. Part 2 waits for that.

### 2026-09-12 · Claude Code

Did: Added a document library indexer as the third offline tool in the kit. It
reads several common document formats, groups their text under whatever headings
they carry, and writes an index file the hub searches alongside the converted
tools. Fixed eight things in how search reads and reports content — most
significantly that HTML was being searched as raw markup, so a word appearing a
hundred times counted as one hit. Added phrase search, lifted the per-document
result cap, added match counts, deduplicated identical files, made a saved index
reopenable, and added size warnings that say plainly when an index has grown past
what belongs on a website.

Learned: The security consequence is the part worth carrying forward. A search
index is a single file containing the full text of everything in it, which makes
it a more concentrated exposure than the documents it indexes. That reframes
gating from a preference to a requirement, and it is better raised before someone
else notices it. The related insight is that gating need not be uniform — the
content used at the worst moment for a login is also the content that does not
need one.

Left off at: Hub running locally, one document converted, library search working.
The indexer work is not yet committed. Nothing deployed. The subdomain request
remains the only blocker nothing else can route around.

### 2026-09-11 · Claude Code

Did: Completed the core feature set — collapsible sections, offline full-text
search, automatic link detection, rebuilt contact cards, and a standalone icon
maker. Converted, committed, and tested against the first real document. Settled
the hosting strategy.

Learned: The most valuable finding was not technical. The first document is
complete and clear, but it is a reference document being used as an operating
procedure, and on a phone at the back of a room it is far too much to hold at
once. Several hours were also lost to duplicate working folders, downloads sharing
filenames, and a service worker serving stale bundles — which produced four
standing rules: one folder, one terminal, one browser tab; bump the service worker
version on every change; commit working state before adding anything; never ship
two bundles with the same filename.

Left off at: Hub built and running locally, first document committed, hosting
plan agreed, deployment blocked on the subdomain.
