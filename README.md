# Cinema Catalogs — Turkish & Russian Sites

A companion **catalog add-on** for Nuvio. It adds five browsing rows from the websites' actual listings, alongside your existing official Nuvio catalog and playback plugins. No PC, scraping server, account credentials or private API keys are needed to use the published catalog.

## Install

Add this URL under Nuvio's **Add-ons**, rather than its JavaScript Plugins section:

```text
https://raw.githubusercontent.com/kratoskrator/cinema-catalogs-nuvio/main/manifest.json
```

Keep the **official Nuvio catalog enabled**. Open the new rows on Home or choose them in Discover. Select a title, choose an episode when applicable, and use Russian Cinema, DiziBOX or DiziYou to look for playback sources.

The companion supplies IMDb identities and posters. The official catalog supplies current descriptions, episode lists and general search. The existing playback plugins perform their normal IMDb-to-TMDB conversion. The companion declares only the `catalog` resource, so it does not replace your metadata or streaming providers.

## Initial snapshot

Website listings were checked on **17 October 2026**. The first release includes **93 cards** across five rows:

| Row | Cards |
| --- | ---: |
| Filmix — Movies | 10 |
| Filmix — Series | 10 |
| Seasonvar — Series | 19 |
| DiziBOX — Series | 28 |
| DiziYou — Series | 26 |

These are selected, verified listings from the captured website pages, not a complete index of every title on each site. Source order is preserved. Seasonvar duplicates across season pages are combined into one show. Each card has its source URL and the date its listing was checked. [snapshot.json](./snapshot.json) records the title-to-ID mapping and provenance.

Matches require an exact normalized title, release year and content type, or an explicitly published external ID verified against the official metadata endpoint. Unmatched titles, ambiguous remakes, stale-only records and episode aliases that the current playback plugin cannot follow are excluded. Display punctuation is made safe for the current TV catalog renderer.

**Catalog membership does not guarantee playback.** A website can publish a title or episode page before a working stream is available. Some listed works may have restricted audio, quality or geographic access. Playback is checked by the selected provider when you open its source list.

Rezka is excluded: normal TV-style requests returned browser verification and browser site-safety policy blocked reading its catalog. HDFilmCehennemi is excluded because the current homepage request returned an access challenge; yesterday's cached Inception page was not treated as a current catalog listing. No challenge was solved or bypassed.

## Freshness and search

This version is a **published snapshot**, not an automatically refreshed live index. Refreshing the add-on downloads the latest published files; it does not crawl the source websites. A maintainer must collect, verify, rebuild and publish a new snapshot to change its cards.

General title search remains with your official catalog. This companion does not advertise its own search endpoint: static GitHub hosting cannot answer arbitrary search queries. It also does not advertise genre filters that it cannot serve. Each complete row has an empty terminal pagination response for Nuvio's Discover screen.

## Validation

All **14 automated tests pass**. The build checks canonical IDs, content types, years, safe source/image URLs, website host provenance, duplicate identities, row routes and terminal pages. Collector tests cover exact matching, first-season years, source order and challenge blocking. Independent checks using current official Nuvio code loaded all five rows and their terminal pages, confirmed Home eligibility, opened actual official metadata for the first card in each row, and preserved exact episode selection through playback-plugin dispatch.

Live extraction and metadata checks used ordinary public requests without account credentials or video downloads. The collectors were also replayed against captured real responses. Physical display and playback on a Samsung TV remain unverified.

## Rebuild or refresh

Download [source.zip](./source.zip). Node.js **20 or newer** is needed only for maintenance, with no package installation required. Reproduce the included snapshot with:

```text
npm run build
npm test
```

Collect a new snapshot into a fresh scratch directory:

```text
node tools/russian/russian-sources.cjs work/russian
node tools/turkish/collect.cjs --out work/turkish --limit 30
node tools/turkish/map.cjs --out work/turkish
node tools/import.cjs work/russian/filmix-mapped.json work/russian/seasonvar-mapped.json work/turkish/dizibox-mapped-records.json work/turkish/diziyou-mapped-records.json
npm run build
npm test
```

Review the generated counts and exclusions before publishing. The collectors are deliberately bounded and stop a source when verification or access restrictions appear. They do not use accounts, execute site scripts, solve challenges, disable certificate validation or request video files.

Publish `manifest.json`, `catalog/`, `snapshot.json`, this README, the license/notices and the source archive together. When row counts change, replace the old generated `catalog/` tree so obsolete terminal routes do not remain. Keep raw HTML captures, metadata caches, local logs and scratch files out of the public repository.

MIT licensed. See [THIRD_PARTY_NOTICES.md](./THIRD_PARTY_NOTICES.md). The add-on is independent of Nuvio and the listed websites.
