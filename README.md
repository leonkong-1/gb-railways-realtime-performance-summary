# GB Railways Real-Time Performance Summary

A single-file web dashboard providing a live visual summary of GB passenger rail punctuality and cancellation performance. Designed to run full-screen on a wall display, and responsive for mobile browsing.

**Live:** [leonkong-1.github.io/gb-railways-realtime-performance-summary](https://leonkong-1.github.io/gb-railways-realtime-performance-summary/)

## Data source

Powered by the **NWR Realtime Performance Data API** from [Rail Data Marketplace](https://raildata.org.uk/dataProduct/P-8b6fb11c-1594-4499-bdc9-383402b460d3/overview). The API delivers rolling real-time on-the-minute performance data across all franchised train operating companies.

## Metrics

The dashboard focuses exclusively on two metrics:

- **Time to 3** — the percentage of trains arriving within 3 minutes of schedule. This is the primary punctuality measure underpinning the current government's regulated performance targets for passenger rail.
- **Cancellations** — the percentage of scheduled services cancelled.

Both are shown at national level in the header and per-TOC in the grid, colour-coded green / amber / red. Only franchised operators are shown; open-access operators and sector-level aggregates are excluded.

## Features

- Live data refreshed every 15 seconds
- Sort by Time to 3 or Cancellations, worst-first or best-first
- Card border colour reflects the active sort metric
- Metric font sizes scale dynamically to fit however many TOCs the API returns
- Responsive: 3-column fixed layout on desktop / wall display; 2-column scrollable on mobile

## Usage

No build step, no server, no dependencies. Open `index.html` directly in Chrome, or visit the GitHub Pages URL above.

To substitute your own API key, replace the value of `API_KEY` near the top of the `<script>` block.

## API key

The API key is embedded directly in the HTML. This is intentional: the underlying data is genuinely open public data — Rail Data Marketplace simply requires a free account registration to obtain a key. The key has no meaningful security value.

## RAG thresholds

| Metric | Green | Amber | Red |
|---|---|---|---|
| Time to 3 | ≥ 85% | 80–85% | < 80% |
| Cancellations | ≤ 2% | 2–4% | > 4% |
