# Catalog format

`catalog.json` uses `schema_version: 1`.

| Field | Meaning |
|---|---|
| status | `published-snapshot`; older empty bootstrap exports may contain `prelaunch` |
| source | Canonical website library URL |
| exported_at | UTC time of the last content change; unchanged runs preserve it |
| count | Number of recordings in this snapshot |
| recordings | Array of published recording entries |

Each entry includes `id`, `title`, `description`, `category`, `tags`, optional-text `location`, `equipment`, `recorded_on` (recording date, `YYYY-MM-DD` or empty), `production_note`, `duration_seconds`, `format` (MIME), `size_bytes`, `creator` (name and public URL), `license` (identifier and URL), `page_url`, `download_url`, `published_at` and `updated_at`.

Titles and descriptions retain the creator's published language. File bytes are not part of this repository. Fetch through the first-party website URLs and handle HTTP 404 as a possible withdrawal. A failed website export must not overwrite the last valid catalog with an empty list. A successful empty public snapshot removes withdrawn recordings from the current catalog and locale bundles; Git history is not rewritten.

## Translation bundles

`translations/<locale>.json` uses `schema_version: 1`, `source`, `source_language`, `fingerprint_version: 1`, `locale` and `recordings`. Each recording has `id`, `source_hash`, `title`, `description`, `category`, `tags`, `location` and `production_note`. The category retains the original code; translated human labels can be supplied by a consuming application. Device, recording date and creator credit must be read unchanged from `catalog.json`.

The SHA-256 fingerprint includes the fingerprint version and original `title`, `description`, `tags`, `category`, `location`, `production_note` and `source_language`. Device, date, attribution and publication timestamps do not trigger retranslation. Empty fields remain empty. Only completed translations matching the current original are exported. There are 14 target locales from the website's current 15-language list, excluding the source language (`zh-Hans` by default).

`translations/index.json` contains `schema_version`, `source`, `source_language`, `fingerprint_version` and `recordings`. Each recording contains `id`, `source_hash`, `locales`, `translation_hash` (SHA-256 of the actual locale entries in website language order), and `translated_at` (ISO UTC). Translation content changes update its hash and date; unchanged runs preserve both. Recording dates remain independent.

The existing Codex scheduled task prepares and translates new or changed public text every day at 09:00 Beijing time, then applies and publishes the validated repository changes. There is no translation API key or paid external translation service in the synchronization script. The manifest and all locale bundles are validated and published in the same Git commit. The website Workers reader checks the manifest against the current D1 source fingerprint for language discovery, hreflang and sitemap; it validates the requested locale bundle independently before rendering its body. Missing or outdated requested text falls back to the original, without making other languages depend on that fetch. Fixed-source public JSON is cached for about 60 seconds. After pushing, the task verifies actual language URLs and sitemap before search submission. GitHub publication alone is not website verification. UI optimization is handled separately.

For maintainers: the website repository owns `scripts/library-translation-sync.mjs prepare --repo DIR --work PLAN` and `apply --repo DIR --work PLAN --translations ANSWERS`. Both read the anonymous production `/api/library/catalog` with cursor pagination. Apply refetches public state, validates all translations, and constructs every output before writing managed files. Unchanged content leaves no diff. The script does not commit or push; the scheduled Codex task reviews the changes and pushes the independent catalog repository. The website's `library:export` remains available for a source-only export.
