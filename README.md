Below are **production-ready, repo-ready** files for a proper public release:

* **README.md** (fully framed for non-technical, technical, and philosophical audiences)
* **LICENSE** (**Apache-2.0** — best balance of *max adoption* + *patent clarity* + *serious builder credibility*)
* **NOTICE** (recommended companion for Apache-2.0)
* **RELEASE_NOTES.md** (copy/paste into a GitHub Release)

---

````md
# README.md

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

````

---

```text
LICENSE
                                 Apache License
                           Version 2.0, January 2004
                        http://www.apache.org/licenses/

   TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION

   1. Definitions.

      "License" shall mean the terms and conditions for use, reproduction,
      and distribution as defined by Sections 1 through 9 of this document.

      "Licensor" shall mean the copyright owner or entity authorized by
      the copyright owner that is granting the License.

      "Legal Entity" shall mean the union of the acting entity and all
      other entities that control, are controlled by, or are under common
      control with that entity. For the purposes of this definition,
      "control" means (i) the power, direct or indirect, to cause the
      direction or management of such entity, whether by contract or
      otherwise, or (ii) ownership of fifty percent (50%) or more of the
      outstanding shares, or (iii) beneficial ownership of such entity.

      "You" (or "Your") shall mean an individual or Legal Entity
      exercising permissions granted by this License.

      "Source" form shall mean the preferred form for making modifications,
      including but not limited to software source code, documentation
      source, and configuration files.

      "Object" form shall mean any form resulting from mechanical
      transformation or translation of a Source form, including but
      not limited to compiled object code, generated documentation,
      and conversions to other media types.

      "Work" shall mean the work of authorship, whether in Source or
      Object form, made available under the License, as indicated by a
      copyright notice that is included in or attached to the work
      (an example is provided in the Appendix below).

      "Derivative Works" shall mean any work, whether in Source or Object
      form, that is based on (or derived from) the Work and for which the
      editorial revisions, annotations, elaborations, or other modifications
      represent, as a whole, an original work of authorship. For the purposes
      of this License, Derivative Works shall not include works that remain
      separable from, or merely link (or bind by name) to the interfaces of,
      the Work and Derivative Works thereof.

      "Contribution" shall mean any work of authorship, including
      the original version of the Work and any modifications or additions
      to that Work or Derivative Works thereof, that is intentionally
      submitted to Licensor for inclusion in the Work by the copyright owner
      or by an individual or Legal Entity authorized to submit on behalf of
      the copyright owner. For the purposes of this definition, "submitted"
      means any form of electronic, verbal, or written communication sent
      to the Licensor or its representatives, including but not limited to
      communication on electronic mailing lists, source code control systems,
      and issue tracking systems that are managed by, or on behalf of, the
      Licensor for the purpose of discussing and improving the Work, but
      excluding communication that is conspicuously marked or otherwise
      designated in writing by the copyright owner as "Not a Contribution."

      "Contributor" shall mean Licensor and any individual or Legal Entity
      on behalf of whom a Contribution has been received by Licensor and
      subsequently incorporated within the Work.

   2. Grant of Copyright License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      copyright license to reproduce, prepare Derivative Works of,
      publicly display, publicly perform, sublicense, and distribute the
      Work and such Derivative Works in Source or Object form.

   3. Grant of Patent License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      (except as stated in this section) patent license to make, have made,
      use, offer to sell, sell, import, and otherwise transfer the Work,
      where such license applies only to those patent claims licensable
      by such Contributor that are necessarily infringed by their
      Contribution(s) alone or by combination of their Contribution(s)
      with the Work to which such Contribution(s) was submitted. If You
      institute patent litigation against any entity (including a
      cross-claim or counterclaim in a lawsuit) alleging that the Work
      or a Contribution incorporated within the Work constitutes direct
      or contributory patent infringement, then any patent licenses
      granted to You under this License for that Work shall terminate
      as of the date such litigation is filed.

   4. Redistribution. You may reproduce and distribute copies of the
      Work or Derivative Works thereof in any medium, with or without
      modifications, and in Source or Object form, provided that You
      meet the following conditions:

      (a) You must give any other recipients of the Work or
          Derivative Works a copy of this License; and

      (b) You must cause any modified files to carry prominent notices
          stating that You changed the files; and

      (c) You must retain, in the Source form of any Derivative Works
          that You distribute, all copyright, patent, trademark, and
          attribution notices from the Source form of the Work,
          excluding those notices that do not pertain to any part of
          the Derivative Works; and

      (d) If the Work includes a "NOTICE" text file as part of its
          distribution, then any Derivative Works that You distribute must
          include a readable copy of the attribution notices contained
          within such NOTICE file, excluding those notices that do not
          pertain to any part of the Derivative Works, in at least one
          of the following places: within a NOTICE text file distributed
          as part of the Derivative Works; within the Source form or
          documentation, if provided along with the Derivative Works; or,
          within a display generated by the Derivative Works, if and
          wherever such third-party notices normally appear. The contents
          of the NOTICE file are for informational purposes only and
          do not modify the License. You may add Your own attribution
          notices within Derivative Works that You distribute, alongside
          or as an addendum to the NOTICE text from the Work, provided
          that such additional attribution notices cannot be construed
          as modifying the License.

      You may add Your own copyright statement to Your modifications and
      may provide additional or different license terms and conditions
      for use, reproduction, or distribution of Your modifications, or
      for any such Derivative Works as a whole, provided Your use,
      reproduction, and distribution of the Work otherwise complies with
      the conditions stated in this License.

   5. Submission of Contributions. Unless You explicitly state otherwise,
      any Contribution intentionally submitted for inclusion in the Work
      by You to the Licensor shall be under the terms and conditions of
      this License, without any additional terms or conditions.
      Notwithstanding the above, nothing herein shall supersede or modify
      the terms of any separate license agreement you may have executed
      with Licensor regarding such Contributions.

   6. Trademarks. This License does not grant permission to use the trade
      names, trademarks, service marks, or product names of the Licensor,
      except as required for reasonable and customary use in describing the
      origin of the Work and reproducing the content of the NOTICE file.

   7. Disclaimer of Warranty. Unless required by applicable law or
      agreed to in writing, Licensor provides the Work (and each
      Contributor provides its Contributions) on an "AS IS" BASIS,
      WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
      implied, including, without limitation, any warranties or conditions
      of TITLE, NON-INFRINGEMENT, MERCHANTABILITY, or FITNESS FOR A
      PARTICULAR PURPOSE. You are solely responsible for determining the
      appropriateness of using or redistributing the Work and assume any
      risks associated with Your exercise of permissions under this License.

   8. Limitation of Liability. In no event and under no legal theory,
      whether in tort (including negligence), contract, or otherwise,
      unless required by applicable law (such as deliberate and grossly
      negligent acts) or agreed to in writing, shall any Contributor be
      liable to You for damages, including any direct, indirect, special,
      incidental, or consequential damages of any character arising as a
      result of this License or out of the use or inability to use the
      Work (including but not limited to damages for loss of goodwill,
      work stoppage, computer failure or malfunction, or any and all
      other commercial damages or losses), even if such Contributor
      has been advised of the possibility of such damages.

   9. Accepting Warranty or Additional Liability. While redistributing
      the Work or Derivative Works thereof, You may choose to offer,
      and charge a fee for, acceptance of support, warranty, indemnity,
      or other liability obligations and/or rights consistent with this
      License. However, in accepting such obligations, You may act only
      on Your own behalf and on Your sole responsibility, not on behalf
      of any other Contributor, and only if You agree to indemnify,
      defend, and hold each Contributor harmless for any liability
      incurred by, or claims asserted against, such Contributor by reason
      of your accepting any such warranty or additional liability.

   END OF TERMS AND CONDITIONS


   Copyright [2026] [BRIAN JOSEPH KLOCK]

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.
````

---

```text
NOTICE

PBI Memory Krystal — Offline Explorer
Copyright 2026 BJ Klock (Kai Rex Klok)

This product includes software developed by BJ Klock (Kai Rex Klok).
Licensed under the Apache License, Version 2.0.
```

---

```md
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
```

---

