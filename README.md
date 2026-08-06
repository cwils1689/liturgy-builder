# LiturgyForge

A drag-and-drop liturgy planner for Reformed churches, built for [Pillar Reformed Church](https://github.com/cwils1689)'s Covenant Renewal Worship and designed to be usable by other congregations too.

**Live:** https://cwils1689.github.io/liturgyforge/
**Status:** Phase 1 complete — usable for Pillar's own weekly planning, open for outside churches to test and evaluate.

---

## What it does

- **Builder** — drag-and-drop liturgy elements (hymns, scripture, prayers, sermon, lectionary readings, exhortations, custom text) into a service order, with rich-text editing in place
- **Planner** — a spreadsheet-style schedule for planning services across weeks/months, with columns for ministers, sermon series, hymn selections, and more
- **Hymnals** — three built-in hymnal datasets you can search and insert directly into a service:
  - Treasury of Psalms & Hymns — 1,136 songs (default)
  - Trinity Hymnal (1990) — ~742 entries, majority-lyrics populated from public-domain 1961 sources
  - Cantus Christi (2020) — ~744 entries (metadata; lyrics not yet loaded)
- **Playback** — piano accompaniment via Tone.js with adjustable tempo, for previewing hymn tunes
- **Export** — Print/PDF, Word (.docx, hand-built via JSZip/OOXML), and a full-screen Presentation Mode for use during the service
- **Cloud sync** — Supabase-backed accounts for signed-in users; fully local-only and private for anyone browsing signed out (no real church data is exposed to guests)

## Tech stack

- Vanilla JavaScript + HTML5 (no framework), single `index.html`
- [Sortable.js](https://sortablejs.github.io/Sortable/) for drag-and-drop
- [Supabase](https://supabase.com/) for auth and cloud sync (chosen over Firebase for privacy)
- [Tone.js](https://tonejs.github.io/) for hymn playback
- [JSZip](https://stuk.github.io/jszip/) for DOCX export
- Integrations: RCL/BCP lectionary data, ESV/KJV Bible API, hymnal metadata sourced in part from Hymnary.org

## Project status

**Phase 1 (complete):** Core Builder + Planner functionality, two hymnals merged with searchable metadata and (partial) lyrics, guest/signed-out mode that's fully local and isolated from real church data, exports working, deployed and in active use by Pillar.

**Currently paused for real-world testing.** The plan is to gather feedback from Pillar's own use and from other pastors trying it out before committing to the next phase.

**Phase 2 (planned, not started):** Multichurch backend — each congregation gets its own isolated account and data via Supabase, rather than the current single-church-plus-guest-mode model. New churches will be provisioned manually at first rather than through open self-serve signup, to validate the data model before building a public-facing flow.

Also deferred to a later phase: Cantus Christi lyrics/indexing, and lyrics for the ~190 Trinity Hymnal 1990 entries not covered by the current public-domain source data.

## Architecture notes

The app is single-tenant today (Pillar Reformed Church), with a small number of isolated constants holding Pillar-specific data:

- `PILLAR_TEMPLATE` — Pillar's actual liturgy content, seeded once into `liturgyTemplates['Covenant Renewal Worship']` via `seedPillarTemplateOnce()`
- `PILLAR_DEFAULT_SCHEDULE_COLUMNS` — Pillar's full 21-column Planner layout
- `SCHEDULE_SEED_DATA` — Pillar's 2025-2026 Planner data (currently dormant/unused)

Everything else — `DEFAULT_TEMPLATE`, `GENERIC_DEFAULT_SCHEDULE_COLUMNS`, `churchName` — is already generic and shared, by design, so that guest/signed-out use never exposes Pillar's real data. When multichurch support is built, the plan is to migrate these three constants into per-church seed data rather than rewrite the surrounding logic.

## Deployment

This is a static site served via GitHub Pages from the repo root (`index.html`). To deploy an update:

1. Download the updated file
2. Replace `index.html` in the repo root
3. Commit — live in about a minute

## Interested in testing?

If you're part of a church considering using this for your own liturgy planning, reach out — testing feedback from real use is exactly what's needed to shape the next phase.

## License

Copyright © 2026 Pillar Reformed Church. All rights reserved.

This software and its contents are proprietary. No part of this repository may be copied, modified, distributed, or used without express written permission from Pillar Reformed Church.
