# Publication rules

This repository is PUBLIC. Assume every file has a public audience. Treat it as
a projection of internal work, not as a place where internal work is authored.

## Never publish

- Scraper internals: endpoints, host names, application IDs, selectors, auth flow,
  rate-limit behavior, or anything that would let a reader reconstruct a pipeline.
- Record content from any data corpus (FAA AIDS, FAA SDR, NTSB, NASA ASRS,
  Transport Canada CADORS, BTS). Not even a single illustrative record.
- Client names, engagement details, or anything about company business, revenue,
  pricing, staffing, or internal politics.
- Unpublished findings intended for publication elsewhere. Reference the work by
  name and status only.
- Credentials, tokens, keys, API endpoints, internal URLs, absolute local paths,
  or hostnames.
- Third-party names in any evaluative context.

## Safe to publish

- Project names, one-paragraph briefs, and status.
- Task titles, task states, and blockers phrased in general terms.
- Architectural decisions and the reasoning behind them.
- Open questions intended for a planning session.
- Session summaries at the level of "what changed and what's next."

## Test before writing any line

Would I say this sentence out loud, unprompted, at an industry conference?
If there is any hesitation, it belongs in internal notes instead.

This repo sits under the company GitHub organization, so anything in it is
publicly attributable to the company, not to an individual. Write accordingly:
plain, professional, no venting, no half-formed opinions about outside parties.

## If something leaks

Public git history is permanent. Removing a file is not enough. A leak requires
history rewrite plus rotation of anything exposed. Assume any secret that lands
here is already burned.
