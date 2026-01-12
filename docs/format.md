# PBI-KRYSTAL-HTML-1.0 — Memory Krystal Offline Explorer Format

This document specifies the **portable data format** consumed by **PBI Memory Krystal — Offline Explorer**.

The goal of this format is simple:

> Package a Memory Krystal (sigil registry / memory log) into a **single JSON object** that can be embedded into a **single HTML file**, enabling **offline search + neural graph navigation + inspection** with zero external dependencies.

---

## 1) Design principles

### 1.1 Portable
A Krystal bundle must be movable as a file:
- no database
- no server requirement
- no environment assumptions

### 1.2 Offline-first
Consumers should render useful state without network access.

### 1.3 Deterministic identifiers
Nodes use stable integer IDs (recommended 0..N-1), enabling compact edges and fast lookups.

### 1.4 Forward-compatible
New fields may be added without breaking older renderers (see Compatibility).

---

## 2) Top-level JSON shape

A **PBI-KRYSTAL-HTML-1.0** document is a single JSON object:

```json
{
  "meta": { ... },
  "nodes": [ ... ],
  "edges": [ ... ]
}
````

### 2.1 `meta` (required)

The `meta` object describes the bundle and provides basic integrity expectations.

**Fields**

* `v` (string, required)
  Must equal: `"PBI-KRYSTAL-HTML-1.0"`
* `generated` (string, required)
  ISO date or ISO datetime string (generator-defined; typically `YYYY-MM-DD`).
* `count` (number, required)
  Declared node count (should match `nodes.length`).
* `edges` (number, required)
  Declared edge count (should match `edges.length`).
* `source` (string, optional)
  Human-readable origin label (e.g. the original registry filename).

**Example**

```json
{
  "v": "PBI-KRYSTAL-HTML-1.0",
  "generated": "2026-01-12",
  "count": 959,
  "edges": 134,
  "source": "sigil-registry-1768196786314.json"
}
```

---

## 3) Nodes

`nodes` is an array of node objects. Each node represents one memory item (sigil, stream entry, URL, transfer, note, etc).

```json
{
  "id": 0,
  "u": "https://…",
  "k": "sigil",
  "p": 9876419,
  "b": 23,
  "s": 15,
  "c": "Root",
  "pk": "…",
  "ks": "…",
  "t": "…",
  "ph": "…",
  "uh": "…"
}
```

### 3.1 Node field reference

| Field | Type                      | Required | Meaning                                                                                 |
| ----: | ------------------------- | :------: | --------------------------------------------------------------------------------------- |
|  `id` | number (int)              |     ✅    | Unique node ID. Recommended contiguous 0..N-1.                                          |
|   `u` | string                    |     ✅    | Primary identifier, usually a URL. Treated as opaque by consumers.                      |
|   `k` | string                    |     ✅    | Kind/category of node. See **3.2**.                                                     |
|   `p` | number (int) | null       |     ✅    | Kai pulse (if applicable). Often present for `sigil`; may be null for `stream` entries. |
|   `b` | number (int 0..35) | null |     ✅    | Beat index (if applicable).                                                             |
|   `s` | number (int 0..43) | null |     ✅    | Step index (if applicable).                                                             |
|   `c` | string | null             |     ✅    | Chakra/category label (if applicable).                                                  |
|  `pk` | string | null             |     ✅    | ΦKey (if present).                                                                      |
|  `ks` | string | null             |     ✅    | KaiSig short (if present). Typically short hex.                                         |
|   `t` | string | null             |     ✅    | Optional text payload / snippet / title (if present).                                   |
|  `ph` | string | null             |     ✅    | Payload hash (if present). Typically 64 hex chars.                                      |
|  `uh` | string | null             |     ✅    | URL hash (if present). Typically 64 hex chars.                                          |

> Note: In 1.0, fields are present but may be `null`. This keeps node parsing uniform and fast.

---

### 3.2 Node kinds (`k`)

`k` is a short string identifying how the renderer should treat the node.

**Common kinds**

* `sigil`
  A sigil / artifact node. Typically has `p`, `b`, `s`, `c` present, and may include `pk`, `ks`, `uh`, `ph`.
* `stream`
  A stream entry node. Often only has `id`, `u`, `k` and other fields are null.
* `other`
  Any node not strictly a sigil or stream entry (notes, derived payloads, partial captures, exports, etc).

**Compatibility rule:** consumers MUST treat unknown `k` values as `other` for rendering.

---

### 3.3 Normalization rules (recommended)

These are recommended generator rules to keep datasets clean:

* `id` SHOULD be stable and unique.
* `id` SHOULD be contiguous integers `0..nodes.length-1` (best for memory + speed).
* `p` SHOULD be an integer pulse when known; otherwise null.
* `b` MUST be `0..35` when present.
* `s` MUST be `0..43` when present.
* `ks` SHOULD be short, display-safe (e.g., first 10 hex) when present.
* `ph`/`uh` SHOULD be lowercase hex if used.

---

## 4) Edges

`edges` is an array of 2-integer pairs:

```json
"edges": [
  [50, 51],
  [81, 80]
]
```

Each pair links two nodes by `id`.

### 4.1 Semantics

In **PBI-KRYSTAL-HTML-1.0**, an edge means:

> “These two nodes are related.”

Edge meaning is intentionally minimal to keep the format compact and broadly usable.

* Edges MAY be interpreted as undirected (typical visualization behavior).
* Generators MAY treat `[a, b]` as directional (a → b) internally, but consumers should not require direction for correct rendering.

### 4.2 Constraints

* Each edge MUST be a 2-element array of integers: `[fromId, toId]`.
* Each referenced ID MUST exist in `nodes`.
* Self-edges `[x, x]` SHOULD be omitted.

---

## 5) Embedding into a single HTML file

The canonical embedding method is:

```html
<script id="KRYSTAL" type="application/json">
{ ...PBI-KRYSTAL JSON... }
</script>
```

### 5.1 Requirements

* The embedded JSON MUST be valid JSON (no trailing commas, no comments).
* The script tag MUST use `type="application/json"` to prevent execution.
* The `id` SHOULD be `"KRYSTAL"` to match common loaders.

### 5.2 Alternate loaders (optional)

A viewer may also support:

* drag-and-drop loading of an external `.json`
* URL-based loading via `fetch()`

These are NOT required by the 1.0 spec, but are compatible with it.

---

## 6) Offline deep-link behavior (PWA-installed routing)

The `u` field often contains URLs.

In this ecosystem, opening a URL can remain **fully offline** if:

* the target route belongs to an **installed PWA** (installed from localhost or a global domain), and
* the PWA has cached its app shell (Service Worker), and
* the route can render using locally available state (URL payload and/or Krystal-local data).

This enables an offline flow:
**Krystal → Offline Explorer → Open URL → installed PWA renders on-device**

**Important:** this behavior depends on the PWA’s caching strategy and is outside the scope of the JSON schema itself. The schema simply stores the URL; offline resolution is a runtime capability.

---

## 7) Compatibility & versioning

### 7.1 Version field

`meta.v` is the format identifier.

* `PBI-KRYSTAL-HTML-1.0` indicates this document follows this spec.

### 7.2 Forward compatibility rules

Consumers:

* MUST ignore unknown top-level keys (future expansion).
* MUST ignore unknown node keys.
* MUST treat unknown `k` as `other`.

Generators:

* MAY add fields in a backward-compatible way (optional keys or nullables).
* MUST bump `meta.v` only for breaking changes.

---

## 8) Security & privacy considerations

* This format is designed to be runnable offline. Treat a Krystal like a dataset:

  * redact private data before publishing
  * assume the file may be shared widely once released
* URLs are user-initiated actions. A viewer should only open URLs on explicit click/tap.
* Hash fields (`ph`, `uh`) are safe to share, but what they refer to might not be.

---

## 9) Minimal example

```json
{
  "meta": {
    "v": "PBI-KRYSTAL-HTML-1.0",
    "generated": "2026-01-12",
    "count": 2,
    "edges": 1,
    "source": "example.json"
  },
  "nodes": [
    {
      "id": 0,
      "u": "https://example.local/sigil/0",
      "k": "sigil",
      "p": 10000001,
      "b": 10,
      "s": 22,
      "c": "Root",
      "pk": "13SGLS…",
      "ks": "6bcfbb0a90",
      "t": null,
      "ph": null,
      "uh": "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa"
    },
    {
      "id": 1,
      "u": "https://example.local/stream/1",
      "k": "stream",
      "p": null,
      "b": null,
      "s": null,
      "c": null,
      "pk": null,
      "ks": null,
      "t": null,
      "ph": null,
      "uh": null
    }
  ],
  "edges": [
    [0, 1]
  ]
}
```

---

## 10) Notes for generators

If you’re generating Krystals for this format, the highest leverage choices are:

* Keep `id` contiguous for speed and memory.
* Use `k` consistently (`sigil`, `stream`, `other`) for predictable UX.
* Include `p/b/s/c` whenever the item is pulse-addressable.
* Include `pk/ks` when identity is known.
* Use `ph/uh` when you want stable referential anchors.

That’s it. Keep it small, fast, and offline.

