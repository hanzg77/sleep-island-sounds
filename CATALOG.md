# Catalog format

`catalog.json` uses `schema_version: 1`.

| Field | Meaning |
|---|---|
| status | `prelaunch` or `published-snapshot` |
| source | Canonical website library URL |
| exported_at | UTC export time; null for a prelaunch placeholder |
| count | Number of recordings in this snapshot |
| recordings | Array of published recording entries |

Each entry includes `id`, `title`, `description`, `category`, `tags`, optional-text `location`, `equipment`, `production_note`, `duration_seconds`, `format` (MIME), `size_bytes`, `creator` (name and public URL), `license` (identifier and URL), `page_url`, `download_url`, `published_at` and `updated_at`.

Titles and descriptions retain the creator's published language; the catalog does not fabricate translations. File bytes are not part of this repository. Fetch through the first-party website URLs and handle HTTP 404 as a possible withdrawal. A failed website export must not overwrite the last valid catalog with an empty list.

For maintainers: the website repository owns `npm run library:export -- /path/to/this/repo`. It reads the anonymous production `/api/library/catalog` endpoint with cursor pagination. It replaces the current snapshot only after all pages validate. Inspect the diff before committing. No scheduled synchronization is enabled at this stage.
