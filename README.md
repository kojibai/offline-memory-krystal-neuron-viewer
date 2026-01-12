# PBI Memory Krystal — Offline Explorer

**A single-file, offline “memory OS” that turns a Memory Krystal (sigil registry) into a searchable, navigable neural graph — no server, no database, no dependencies.**

This is not “a page.”
It’s a **portable interpreter for memory**.

You give it a Krystal.
It renders a world.

---

## What this is

This repo ships a **self-contained HTML application** that loads a **Memory Krystal JSON** and renders it as:

- a **fractal search interface** (fast filtering across pulses, ΦKey, KaiSig, chakra/category, text, urls)
- a **neural map** (nodes + links with focus/lineage highlighting)
- a **Focused Memory inspector** (decoded payload view + key fields)
- an **offline export tool** (export filtered JSON slices)

It’s designed to make a Krystal feel like **memory you can *walk through*** — not a file you “open.”

---

## Why this matters (in plain English)

Most “truth,” “identity,” “logs,” and “history” on the internet are:

- stored behind accounts
- served from databases
- verified by platforms
- vulnerable to edits, deletions, drift, outages, and gatekeeping

This project flips that model:

### The object is the system.

A Krystal isn’t “data for an app.”
A Krystal is a **portable memory substrate**, and this HTML file is a **universal offline interpreter**.

If you can hand someone **one file**, and they can immediately *see, search, and traverse* the state — that’s a new medium.

---

## Why it matters (for builders / engineers)

This is effectively:

- **Graph DB** (nodes + edges) with **no DB**
- **Search index** built in-memory at runtime with **no backend**
- **Visualizer + inspector UI** with **no framework**
- **Deterministic replay surface** for state exploration (the file is the artifact)

And because it runs in a browser, you inherit a massive runtime “for free”:
GPU canvas, JS engine, memory management, sandboxing, and distribution to billions of devices.

---

## Features

### Explore
- **Neural map** (pan / zoom / click-to-focus)
- **Lineage highlighting** (focus reveals relationships)
- **List + graph are linked** (click either side)

### Search + filter
- Search across structured fields: pulse, beat, step, chakra/category, ΦKey, KaiSig, text, urls
- Kind filter: **Sigils / Streams / Other**
- Sort options: relevance, pulse asc/desc, kind

### Inspect
- “Focused Memory” panel shows:
  - decoded payload (pretty-printed)
  - canonical fields (kind, pulse, beat, step, chakra/category, keys, hashes when present)
  - “Open URL” action (when node is a URL entry)

### Offline export
- Export **filtered JSON** from the current view, so you can slice a Krystal into smaller “memory shards.”

### No dependencies
- Single HTML file
- No npm, no build step, no external libraries

---

## The hidden superpower: URLs can still resolve *offline* (with the PWA installed)

The “Open URL” action is user-initiated. Normally, opening a URL implies “online.”

But in this ecosystem, if the target URL points to a **PWA route** (localhost or a global domain) *and that PWA is installed on the device*, the link can still render **fully offline**, because:

1. **Installed PWA = cached app shell**
   - The device already has the UI + route handler locally (via Service Worker / install cache).

2. **State can be self-contained**
   - If the route carries its own proof/state in the URL (or the state is present locally via the Krystal), the UI can render without fetching a server.

So the system becomes:
- **offline file → offline explorer → offline deep-link into installed PWA**
- whether that PWA was installed from **localhost** or from a **global state domain**

> Note: The first visit/install must happen while online. After install, the route can run offline as long as the PWA has cached its shell and the link’s required state is present locally (URL payload and/or Krystal).

---

## Quickstart

### Option A — Open the included HTML
1. Download / clone the repo
2. Open the HTML file in a browser (Chrome recommended):
   - `PBI_Memory_Krystal_Offline_Explorer_v5.html`

That’s it.

### Option B — Serve locally (optional)
Some browsers apply stricter file:// policies depending on settings. If you want consistent behavior:

```bash
python3 -m http.server 8080
# then open http://localhost:8080
````

---

## Using your own Memory Krystal

This explorer is designed to be **embeddable** as a single artifact.

### Current embedding model (v5)

The Krystal data is embedded directly inside the HTML as JSON.

Look for a script tag like:

```html
<script id="KRYSTAL" type="application/json">
  { ... }
</script>
```

To swap in a new Krystal:

1. Generate your Krystal JSON (your registry export)
2. Replace the JSON contents inside the `KRYSTAL` script tag
3. Save the HTML — the file is now a complete offline explorer for that new Krystal

> This “data-inside-the-app” pattern is intentional: it creates a single, portable object you can share, archive, hash, and re-open anywhere.

---

## Data model (PBI-KRYSTAL-HTML-1.0)

The embedded JSON includes:

* `meta` (version, generated time, counts, source)
* `nodes[]` (each node is a memory item)
* (optionally) `edges[]` / links references (depending on generator)

Node fields visible in the embedded dataset include (examples):

* `id` (internal node id)
* `u` (url or identifier)
* `k` (kind: sigil / stream / other)
* `p` (pulse)
* `b` (beat)
* `s` (step index)
* `c` (chakra/category)
* `pk` (ΦKey when present)
* `ks` (KaiSig short when present)
* `ph` / `uh` (hash references when present)

The UI surfaces these in both list cards and the Focused Memory inspector.

---

## Security & privacy notes

* **Offline by default.** The explorer is built to run without any network dependency.
* The only “network-ish” behavior is when you click **Open URL** for nodes that contain URLs. That action is user-initiated.
* Because it’s a browser app, it runs in the normal browser sandbox.
* If you publish demo Krystals publicly, treat them like publishing any dataset: redact what you don’t want distributed.

---

## Who this is for

### Non-technical

You want to *feel* what “portable truth” means: not an app, a **shareable memory object**.

### Designers / storytellers

You want a visual medium where memory feels like a living network, not a list.

### Engineers

You want an offline-first, dependency-free proof that a ~4–5MB artifact can behave like an app + database + explorer.

### Auditors / researchers

You want state inspection and traceability in a form that can be archived, hashed, and re-opened years later.

---

## Philosophy (what this repo is really demonstrating)

This explorer is a demonstration of a deeper pattern:

> **Truth as a file format.**
> Not truth as a platform. Not truth as a service.
> Truth as a portable object that can be re-rendered anywhere.

---

## Recommended repo layout

```
/ (root)
  PBI_Memory_Krystal_Offline_Explorer_v5.html
  /examples
    sample_krystal.json
    sample_explorer.html
  /docs
    format.md
    screenshots/
  LICENSE
  NOTICE
  README.md
  RELEASE_NOTES.md
```

---

## Roadmap (optional, but powerful)

* Drag-and-drop “Load Krystal JSON” mode (so the HTML can stay static and load external files)
* Multi-Krystal merge view (overlay 2–N registries and compare lineage)
* Deterministic “memory clustering” (community detection / clustering, rendered as constellations)
* Export bundles: filtered Krystal + companion HTML in one click

---

## Credits

Built and authored by **BJ Klock (Kai Rex Klok)** — as a demonstration of **offline, deterministic, portable memory exploration** rendered from a Krystal registry.
