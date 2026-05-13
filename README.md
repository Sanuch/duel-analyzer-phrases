# Duel Analyzer Phrases Catalog

Phrase patterns for the [Duel Analyzer](https://github.com/YOUR_ORG/duel-analyzer-resources) browser extension.

## Contents

- **`manifest.json`** — Legacy v1 manifest for older extension releases.
- **`manifest.v1.json`** — Alias of the same legacy v1 manifest.
- **`manifest.v2.json`** — New manifest for the current extension line.
- **`resources-v1/`** — Legacy v1 resource files, including `voice-result-groups.json`.
- **`resources/`** — v2 resource files (voice, influence, miracle, conditions) with explicit `pattern/result` entries.
- **`catalog.json`** — Source metadata tracking which phrase came from which recognizer method.
- **`scripts/`** — Development-only tools (requires local logs2 repository to regenerate catalog).

## Usage in Extension

The Duel Analyzer extension loads this manifest at build time by setting the environment variable:

```bash
VITE_PHRASES_MANIFEST_URL=https://raw.githubusercontent.com/YOUR_ORG/duel-analyzer-phrases/main/manifest.v2.json
```

The extension then:
1. Fetches `manifest.v2.json`
2. Downloads each resource file with checksum validation
3. Uses explicit `result` tags from each pattern entry and caches data locally

## Versioning

- `dataVersion` in manifest entries tracks when phrase content changes
- Checksums validate file integrity during download
- Extension only re-downloads files when dataVersion differs from cached version
- Old extension builds should stay on `manifest.json` (v1), new builds must use only `manifest.v2.json`.

## For Maintainers

To regenerate the catalog from source recognizers:

```bash
npm run generate
```

This requires the local logs2 repository and Python 3.12+.
