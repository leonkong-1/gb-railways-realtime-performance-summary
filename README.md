# GBR TOCs Real-Time Performance

A web dashboard showing live GB passenger rail punctuality and cancellation performance across all franchised TOCs. Designed to run full-screen on a wall display, and responsive for mobile browsing. Every TOC has a deep-dive page showing its service-group breakdown; GTR's deep-dive also rolls service groups up into sub-brands.

**Live:** [gbrperformance.uk](https://gbrperformance.uk/)

## Data source

Powered by the **NWR Realtime Performance Data API** from [Rail Data Marketplace](https://raildata.org.uk/dataProduct/P-8b6fb11c-1594-4499-bdc9-383402b460d3/overview). The API delivers rolling real-time on-the-minute performance data across all franchised train operating companies.

## Metrics

- **Time to 3** — percentage of trains arriving within 3 minutes of schedule. The primary punctuality measure underpinning the current government's regulated performance targets for passenger rail.
- **Cancellations** — percentage of scheduled services cancelled.

Both are shown at national level in the header and per-TOC in the grid. Deep-dive pages also show the raw figures behind each percentage (count, totalStops, score, trains). Only franchised operators are shown; open-access operators and sector-level aggregates are excluded.

## Pages

| Page | Purpose |
|---|---|
| `index.html` | Overview of all franchised TOCs. Every TOC card links to its deep-dive. |
| `gtr.html` | GTR deep-dive: GTR Total, three sub-brands (Southern, Thameslink, Great Northern), and their service groups |
| `toc.html?code=<code>` | Deep-dive for any other franchised TOC: TOC Total plus its service groups. Example: `toc.html?code=SWT` for South Western Railway |

## Features

### Overview page (`index.html`)
- Live data refreshed every 15 seconds
- Live clock ticking every second, showing time and date; separate "last updated" timestamp on data refresh
- Header subtitle showing rolling window basis ("Rolling daily totals from 04:30 hours")
- TOCs grouped into sector bands — **Long Distance**, **Regional**, **London & SE** — sorted independently within each sector; non-GBR franchised operators (Caledonian Sleeper, ScotRail, TfW, Elizabeth line, Merseyrail, London Overground) collected into a separate **Non-GBR** band at the bottom
- Sort by Time to 3 or Cancellations, worst-first or best-first; active sort metric leads in each card and drives card border colour
- Card colours (green / red) reflect performance against each TOC's Joint Performance Strategy (JPS) franchise target for FY2026/27; TOCs without a JPS target and the national headline figures are shown in white
- Abbreviated TOC names (e.g. LNER, AWC, ScotRail) from `toc_mapping.csv`
- Time to 3 displayed in **bold (700)**, Cancellations in **light (300)** — visually distinct without colour reliance
- Numbers use tabular figures for stable layout as values update
- Breathing animation on any value that changes between refreshes
- Desktop: 3-column grid, horizontal card layout (name | metric | metric), fixed 40/30/30% column proportions per card
- Mobile: 2-column scrollable layout, vertical card layout
- Every TOC card is clickable and opens its deep-dive page

### Deep-dive pages (`gtr.html` and `toc.html`)
- Pulls from the TOC-specific API endpoint, not the headline endpoint
- **TOC Total row** pinned at the top, coloured green / red against the TOC's JPS target (white where no target exists)
- **Service group rows** shown beneath, with raw figures (count, totalStops, score, trains) alongside percentages for auditability
- **Sort bar:** sort by Time to 3, Count, Stops, Cancellations, Score or Trains, Ascending or Descending. Default is Time to 3, Descending
  - On `toc.html`, service groups sort across the whole TOC
  - On `gtr.html`, service groups sort within each sub-brand; the sub-brand rows stay in their fixed order
- Sub-brand percentages on `gtr.html` are derived by summing raw counts across service groups first, then dividing — not averaging the per-group API percentages
- Column headers truncated on mobile ("Cancellations" → "Cancs", "totalStops" → "stops")
- Same 15 s auto-refresh, breathing animation, and dark aesthetic as the overview page
- Back link returns to `index.html`

## RAG colours

Colours are based on each TOC's JPS franchise target for FY2026/27, not fixed thresholds:

- **Time to 3:** green if above the JPS target, red otherwise
- **Cancellations:** green if below the JPS target, red otherwise
- TOCs without a JPS target (Caledonian Sleeper, London Overground) and the national headline figures are shown in white

Targets are embedded in `index.html`, `gtr.html` and `toc.html`.

## Usage

No build step, no server, no dependencies. Open `index.html` directly in Chrome, or visit the GitHub Pages URL above. Deep-dive pages work the same way; for `toc.html`, add the `?code=` parameter (e.g. `toc.html?code=SWT`).

To substitute your own API key, replace the value of `API_KEY` near the top of the `<script>` block in each page (`index.html`, `gtr.html`, `toc.html`).

## API key

The API key is embedded directly in the HTML. This is intentional: the underlying data is genuinely open public data — Rail Data Marketplace simply requires a free account registration to obtain a key. The key has no meaningful security value.
