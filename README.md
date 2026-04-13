# GBR TOCs Real-Time Performance

A single-file web dashboard showing live GB passenger rail punctuality and cancellation performance across all franchised TOCs. Designed to run full-screen on a wall display, and responsive for mobile browsing.

**Live:** [leonkong-1.github.io/gb-railways-realtime-performance-summary](https://leonkong-1.github.io/gb-railways-realtime-performance-summary/)

## Data source

Powered by the **NWR Realtime Performance Data API** from [Rail Data Marketplace](https://raildata.org.uk/dataProduct/P-8b6fb11c-1594-4499-bdc9-383402b460d3/overview). The API delivers rolling real-time on-the-minute performance data across all franchised train operating companies.

## Metrics

- **Time to 3** — percentage of trains arriving within 3 minutes of schedule. The primary punctuality measure underpinning the current government's regulated performance targets for passenger rail.
- **Cancellations** — percentage of scheduled services cancelled.

Both are shown at national level in the header and per-TOC in the grid, colour-coded green / amber / red. Only franchised operators are shown; open-access operators and sector-level aggregates are excluded.

## Features

- Live data refreshed every 15 seconds
- Live clock ticking every second, showing time and date; separate "last updated" timestamp on data refresh
- Header subtitle showing rolling window basis ("Rolling daily totals from 04:30 hours")
- TOCs grouped into sector bands — **Long Distance**, **Regional**, **London & SE** — sorted independently within each sector; non-GBR franchised operators (Caledonian Sleeper, ScotRail, TfW, Elizabeth line, Merseyrail, London Overground) collected into a separate **Non-GBR** band at the bottom
- Sort by Time to 3 or Cancellations, worst-first or best-first; active sort metric leads in each card and drives card border colour
- Abbreviated TOC names (e.g. LNER, AWC, ScotRail) from `toc_mapping.csv`
- Time to 3 displayed in **bold (700)**, Cancellations in **light (300)** — visually distinct without colour reliance
- Numbers use tabular figures for stable layout as values update
- Breathing animation on any value that changes between refreshes
- Desktop: 3-column grid, horizontal card layout (name | metric | metric), fixed 40/30/30% column proportions per card
- Mobile: 2-column scrollable layout, vertical card layout

## RAG thresholds

| Metric | Green | Amber | Red |
|---|---|---|---|
| Time to 3 | ≥ 85% | 80–85% | < 80% |
| Cancellations | ≤ 2% | 2–4% | > 4% |

## Usage

No build step, no server, no dependencies. Open `index.html` directly in Chrome, or visit the GitHub Pages URL above.

To substitute your own API key, replace the value of `API_KEY` near the top of the `<script>` block.

## API key

The API key is embedded directly in the HTML. This is intentional: the underlying data is genuinely open public data — Rail Data Marketplace simply requires a free account registration to obtain a key. The key has no meaningful security value.
