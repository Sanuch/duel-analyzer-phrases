# Duel Analyzer Phrases Catalog

Phrase patterns for the [Duel Analyzer](https://github.com/YOUR_ORG/duel-analyzer-resources) browser extension.

## Contents

- **`manifest.json`** — Index of all available phrase resources. Used by the extension to discover and load pattern files.
- **`resources/`** — Pattern data files (voice.json, influence.json, miracle.json, conditions.json).
  - Each file contains regex patterns used to recognize battle events in real-time.
  - Language-agnostic: patterns work for both Russian and English text.
- **`catalog.json`** — Source metadata tracking which phrase came from which recognizer method.
- **`scripts/`** — Development-only tools (requires local logs2 repository to regenerate catalog).

## Usage in Extension

The Duel Analyzer extension loads this manifest at build time by setting the environment variable:

```bash
VITE_PHRASES_MANIFEST_URL=https://raw.githubusercontent.com/YOUR_ORG/duel-analyzer-phrases/main/manifest.json
```

The extension then:
1. Fetches `manifest.json`
2. Downloads each resource file with checksum validation
3. Compiles regex patterns and caches them locally

## Versioning

- `dataVersion` in manifest entries tracks when phrase content changes
- Checksums validate file integrity during download
- Extension only re-downloads files when dataVersion differs from cached version

## For Maintainers

To regenerate the catalog from source recognizers:

```bash
npm run generate
```

This requires the local logs2 repository and Python 3.12+.
