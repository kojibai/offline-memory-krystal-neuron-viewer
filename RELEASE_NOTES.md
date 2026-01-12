# RELEASE_NOTES.md

## PBI Memory Krystal — Offline Explorer v5.0.0

**Release Theme:** *Truth as a file format.*

This release packages a Memory Krystal (sigil registry) into a fully interactive **single-file offline explorer** that renders as a fractal search + neural graph + focused inspector — with zero external dependencies.

### Highlights

- **Single HTML artifact**
  - No npm, no build, no backend, no CDN.
  - Open it and you’re inside a living memory field.

- **Fractal Search**
  - Query across pulses, ΦKey, KaiSig, chakra/category, text, and urls.
  - Instant filtering and relevance sorting in-memory.

- **Neural Graph Map**
  - Pan/zoom exploration of node constellations.
  - Click to focus, with lineage/relationship highlighting.

- **Focused Memory Inspector**
  - Decodes payloads into readable structured state.
  - Surfaces canonical fields (kind, pulse, beat, step, chakra/category, keys, hashes when present).
  - “Open URL” action for URL nodes.

- **Offline Export**
  - Export the current filtered view as JSON to create smaller “memory shards.”

### Offline Deep-Link Behavior (PWA Installed)

URLs opened from inside the explorer can still resolve **fully offline** when they point to a route handled by an installed PWA (localhost or a global state domain), because:

- the installed PWA provides the cached app shell, and
- the verification/state needed to render can be carried in the URL and/or already present locally via the Krystal.

This allows an offline flow like:
**Krystal → Offline Explorer → Offline URL → Installed PWA renders on-device**

> Note: Installation must occur while online at least once. After that, offline routing depends on the PWA’s cached shell and locally available state.

### Files

- `PBI_Memory_Krystal_Offline_Explorer_v5.html` — the entire application + embedded Krystal
- `README.md` — full framing + usage + security + philosophy
- `LICENSE` / `NOTICE` — Apache-2.0 release packaging
