# Cinema Catalogs 1.0.1 — 26 October 2026

All 15 automated tests pass. Fresh collectors read public Filmix, DiziBOX and DiziYou listings and verified mapped identities against Nuvio's official metadata service. The final add-on contains 102 cards: 14 Filmix movies, 15 Filmix series, 28 DiziBOX series, 26 DiziYou series, and 19 retained Seasonvar series.

Seasonvar currently serves a technical-maintenance page. Its retained entries keep their original 17 October listing-verification dates. `snapshot.json` records the current maintenance observation separately; no retained entry is presented as a newly verified website listing.

Independent validation loaded the final local files through current official Nuvio add-on mapping, catalog repository, Home and search helpers. All five rows remain Home eligible; the add-on advertises only catalogs and supplies no independent search targets. Every card's IMDb identity, type, year and name matches its provenance record. First-card official metadata for every row returned HTTP 200 with the expected ID/type/year; series metadata included episodes. Five poster URLs returned HTTP 200 with nonempty content lengths.

The current terminal routes are `skip=14`, `skip=15`, `skip=19`, `skip=28` and `skip=26`, each returning an empty `metas` list. Previous Filmix `skip=10` routes remain intentionally empty for clients with cached older rows. They do not add duplicate titles or change the current pagination counts.

The previous public 1.0.0 add-on also passed all five route/terminal/metadata checks; no current Home compatibility bug was found. This release refreshes the four healthy rows, adds explicit outage provenance, and derives the manifest version from the package version.

No site scripts, video files, browser challenges, accounts or private keys were used. Raw captures and metadata caches are excluded from the source archive. This remains a dated static snapshot, not a live index. Physical Samsung rendering and playback are untested; selecting a card still requires a working playback source from the enabled plugins.
