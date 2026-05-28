# SolrWayback Playback POC

A React frontend for browsing archived web pages served by [SolrWayback](https://github.com/netarchivesuite/solrwayback). Search archived pages, play them back in-browser with time-divergence detection, and explore domain-link graphs.

Free and open source.

**Authors:** Nana Oye Akrofi-Quarcoo, Eske Junker, & Jonatan Fuglsang Schwennesen. Master's thesis, Computer Science, Aarhus University.

## Requirements

- Node.js 18+
- A running SolrWayback backend instance running at `http://localhost:8080`, serving WARC files.

## Setup

```bash
npm install
npm run dev
```

Dev server runs at `http://localhost:5173`. Requests to `/solrwayback` are proxied to the backend (see `vite.config.ts`).

## Flow

1. **Search** (`/`) — Query SolrWayback's full-text index. Click a result to open playback.
2. **Playback** (`/playback`) — Archived HTML loads in a sandboxed iframe. Embedded resources are checked for time-divergence and highlighted if they exceed a threshold. Link clicks are intercepted and routed through the app.
3. **Overview** (`/overview`) — An interactive graph built from the domain export. Nodes = pages, edges = links. Click to expand, double-click to mark visited. State syncs across tabs via BroadcastChannel.

## Tested Domain

This prototype has been tested and confirmed working against a real archived domain:

> **[http://kidsinministry.com:80](http://kidsinministry.com:80)**

This is a relatively lightweight site, which makes it well-suited for demonstrating the prototype. The **Overview page** may take a moment to load as it builds the full domain graph. Heavier or more complex sites may experience slower load times or reduced performance when generating the overview — this is expected behaviour at the current prototype stage.
