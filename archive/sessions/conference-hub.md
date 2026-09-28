# Conference Hub · archived sessions

Older entries rolled out of `projects/conference-hub.md`, newest first.

### 2026-09-09 · Claude Code

Did: Built and tested the hub shell and converted the first document. Established
the two-artifact content pipeline — an offline content builder and a structure-only
shape report. Chose the hosting approach and identified the authentication blocker.

Learned: Probing what a stated platform preference actually meant turned out to be
worth the time — it meant "where we already sign in" rather than a technology
mandate, which opened up the approach that wins on offline capability and device
compatibility. Separately, every parser bug found that day was caught by comparing
output against the real document, and the largest one surfaced because a word count
did not add up.

Left off at: Hub shell working, one document converted, not deployed.
