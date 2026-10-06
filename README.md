# Sleep Island · Open Sound Library

[简体中文](README.zh-CN.md) · [Recording catalog](SOUNDS.md) · [Machine-readable catalog](catalog.json) · [Translations](translations/) · [Contributing](CONTRIBUTING.md)

Field recordings from nature and everyday life, with a story, a creator and a clear license. Built for people making games, films, audio tools and other creative projects.

See [SOUNDS.md](SOUNDS.md) for the published inventory in this snapshot. Empty means no public recordings were returned at export time; this is never a sample dataset.

[Visit Sleep Island](https://www.sleepisland.org/?utm_source=github&utm_medium=referral&utm_campaign=open_sound_library)

## What belongs here

- A searchable catalog of published field recordings, with duration, format, file size, creator and license.
- Recording and editing notes, including known voices, music or sudden sounds where identified.
- Attribution examples, corrections and requests for recordings.

Audio and cover files are served by the website using Cloudflare R2. This Git repository contains the catalog and contribution documentation, not the audio archive. The website is the listening, download and submission interface. The Sleep Island app is a separate sleep and relaxation experience; existing app sounds are not automatically part of this collection.

## Using a recording

1. Choose a released recording in [SOUNDS.md](SOUNDS.md), then open its website page.
2. Read the description and license, preview the actual audio and download it without creating an account.
3. Copy its attribution and describe any changes you make.

Open recordings use **CC BY 4.0**, confirmed by their creators. Always check the individual entry. Example attribution (replace the placeholders):

> “Recording title” by Creator — original work URL — CC BY 4.0 (https://creativecommons.org/licenses/by/4.0/). Changes: trimmed and mixed into a game scene.

Public availability can change after a correction or withdrawal. A catalog snapshot is not a promise of permanent hosting. See [LICENSE.md](LICENSE.md) for scope and [CATALOG.md](CATALOG.md) for the data format.

## Daily catalog and translations

Every day at 09:00 Beijing time, the existing Codex scheduled task reads the public website catalog, translates new or changed recording text into the website's other 14 languages, and synchronizes this repository. Original text stays in `catalog.json`; translated titles, descriptions, tags, public locations and production notes are in `translations/<language>.json`. Empty fields stay empty. Creator names, equipment, recording dates and audio are not translated.

Translations are linked to the exact original text by a source fingerprint. Unchanged text is reused; withdrawn recordings leave the current snapshot. A failed fetch or validation preserves the last valid files. `translations/index.json` lists the source fingerprint, available locales, a stable translation-content hash and the last translation change time for each recording.

The manifest and all locale files are validated and published in one Git commit. The website's Workers reader checks the manifest against the current original for language discovery, hreflang and the sound sitemap, and separately validates the requested translation before rendering its page. Its cache is about 60 seconds; missing or outdated requested text falls back to the original without requiring every other language to be fetched. GitHub publication and verified website availability remain separate results. The daily task checks the live language pages and sitemap before search submission. This task does not delay the original recording's publication. Recording pages keep their existing layout; UI optimization is handled separately.

## Help build the collection

Request a sound or report a metadata error through Issues. Contributions can include better descriptions, translations, recording context and examples of creative use. Please do not attach audio, private recordings or personal information to public issues. [Register and upload a recording](https://www.sleepisland.org/library/upload/) on the website. Regular submissions follow the site's review process; trusted creator recordings processed in the local recording desk can be published directly.

**ethan** contributes original field recordings. Check each entry for its actual equipment and recording date. Unreleased material remains private until the creator confirms its release and license. We do not infer recording dates from unverified device timestamps.
