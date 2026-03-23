# GB Railways Real-Time Performance Summary

A single-file web dashboard that provides a live visual summary of GB passenger rail punctuality and cancellation performance, designed to run full-screen on a wall display.

## Data source

Powered by the **NWR Realtime Performance Data API** from [Rail Data Marketplace](https://raildata.org.uk/dataProduct/P-8b6fb11c-1594-4499-bdc9-383402b460d3/overview). The API delivers rolling real-time on-the-minute performance data across all franchised train operating companies.

## Metrics

The dashboard focuses exclusively on two metrics:

- **Time to 3** — the percentage of trains arriving within 3 minutes of schedule (long-distance) or 1 minute (suburban). This is the primary punctuality measure underpinning the current government's regulated performance targets for passenger rail.
- **Cancellations** — the percentage of scheduled services cancelled.

Both metrics are shown at national level in the header and per-TOC in the grid, colour-coded green / amber / red against standard industry thresholds.

Only franchised operators are shown. Open-access operators and sector-level aggregates are excluded.

## Usage

No build step, no server, no dependencies. Open `gb_rail_wall_display.html` directly in Chrome.

The display auto-refreshes every 60 seconds. The sort order (Time to 3 or Cancellations, worst-first or best-first) can be toggled without reloading.

## API key

The API key is embedded directly in the HTML. This is intentional: the underlying data is genuinely open public data — Rail Data Marketplace simply requires a free account registration to obtain a key. The key itself has no meaningful security value. If you want to use your own key, replace the value of `API_KEY` near the top of the `<script>` block.

## RAG thresholds

| Metric | Green | Amber | Red |
|---|---|---|---|
| Time to 3 | ≥ 85% | 80–85% | < 80% |
| Cancellations | ≤ 2% | 2–4% | > 4% |
