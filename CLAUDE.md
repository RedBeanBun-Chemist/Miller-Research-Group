# CLAUDE.md — guidance for AI sessions on this repo

This file is persistent context for Claude (and any other AI assistant) working on the Miller Research Group website. It is distilled from Anthropic's "Why do AI models hallucinate?" guidance and tailored to the specific risks that exist in this repo.

Read this before making edits that touch people, publications, dates, or external links.

---

## 1. Where hallucinations are most likely on this project

The original Anthropic guidance flags these high-risk categories, all of which are present in this repo:

| Category | Examples on this site |
| --- | --- |
| Specific facts & statistics | Publication counts, award years, metric claims ("3.25-fold improved photon delivery", "14,600× the warming potential of CO₂") |
| Citations | Journal names, years, DOIs, author lists in `publications.html` |
| Obscure / niche topics | Individual reaction methodologies, reactor designs |
| Real but not widely known people | Group members' prior affiliations, current positions of alumni |
| Exact details | Dates, degree years, street addresses, room numbers, postcodes |

If you are editing anything in those categories, assume you do not know the answer and look it up.

## 2. Known placeholder data — do not publish as-is

These files contain data that was generated as scaffolding and has **not** been verified against primary sources. Treat every name, date and destination here as unknown until a human has confirmed it.

- **`alumni.html`** — intentionally empty. The earlier fictional PhD and postdoc entries have been removed. Card templates live inside HTML comments in each `.members-grid`; populate with real data only. Do not re-introduce invented names, years, thesis titles, or "Now at…" destinations.
- **`news.html`** — the 2024 JOC award entry and the 2026 Angew. Chem. / React. Chem. Eng. entries were sourced via an earlier agent search. Re-verify the journal, year, volume, issue, page, and DOI before the site goes live.
- **`about.html`** — Philip Miller's career dates (PhD / BSc years, institutions, postdoc location) should be cross-referenced against his [Imperial profile](https://profiles.imperial.ac.uk/philip.miller) and ORCID `0000-0002-8394-2516` before they leave the repo.
- **`publications.html`** — individual publication rows were populated via agent tool search. Re-verify DOIs and author ordering before publishing.
- **`contact.html`** — the map embed uses the address string `Molecular Sciences Research Hub, 82 Wood Lane, London W12 0BZ`. If you ever replace the embed with a coordinate-based version, verify the lat/lon against the Imperial White City campus map (approx. 51.5043°N, 0.2344°W) rather than trusting a generated number.

## 3. Working rules for this repo

### Say "I don't know"
If the user asks for a fact you cannot verify from what is already in the repo or a link they provided, say so. Do not invent a plausible-looking DOI, volume number, date, or postcode. A blank field with a `TODO` comment is always better than a confident fabrication.

### Cite the source in a comment, not just in prose
When you add a fact to the site, leave a trace of where it came from — e.g. `<!-- source: https://profiles.imperial.ac.uk/philip.miller (retrieved YYYY-MM-DD) -->`. If you cannot leave a comment on the surface (e.g. inside a `<title>`), add it to a neighbouring block.

### Flag placeholders unmissably
Use an HTML comment at the top of the section: `<!-- PLACEHOLDER — replace before publishing -->`. Do not rely on the user to remember which rows you made up.

### Prefer repo variables over hard-coded values
Colours, font families and radii live in CSS custom properties in `:root` (`styles.css`). Use `var(--imperial)` rather than re-typing `#003E74` — this keeps the palette self-consistent if it is ever updated again.

### Cross-reference before asserting
When the user asks "does X work?" about something visible (nav links, embed src, file existence), open the file and check. Don't answer from what you remember generating in an earlier turn — the user may have reverted, and the palette has already been reverted once in this project's history.

## 4. Tactics from the source guidance

From Anthropic's "Why do AI models hallucinate?":

1. **Ask for sources.** If you've been handed a claim to put on the site, ask where it came from before you add it.
2. **Check that sources actually support the claim.** A paper exists ≠ a paper says what you think it says.
3. **State confidence explicitly.** "I am confident X" vs "I believe X but have not verified" vs "I don't know" — use all three.
4. **In a fresh chat, ask for errors.** If you are unsure about something you wrote, spin it into its own verification task rather than defending it in the same thread.
5. **For critical text, cross-reference with trusted sources** — Imperial profile, ORCID, DOI resolvers, the journal's own website. Funding-body claims go via the funder's site.
6. **If something sounds off, ask follow-ups** — to the user, not to yourself.

## 5. Source

Full transcript of the Anthropic guidance this file is distilled from: `docs/hallucination-guidance.md`.
