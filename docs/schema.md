# KoshurCorpus Dataset Schema (draft v0.1)

Each entry in the corpus is one record with the following fields. Format:
JSON Lines (`.jsonl`), one record per line — easy to stream, diff, and load
into HF Datasets without custom parsing.

## Core fields

| Field | Type | Required | Notes |
|---|---|---|---|
| `id` | string | yes | Stable unique ID, e.g. `ks-0000001`. Never reused, even if an entry is later removed. |
| `text` | string | yes | The Kashmiri text, in its original script, unmodified. |
| `script` | enum | yes | `arab` (Perso-Arabic/Nastaliq), `deva` (Devanagari), `latn` (Latin transliteration), `sharada` (rare/historical). |
| `translit` | string | no | Optional transliteration into a second script, if available/derived. Never required at ingestion. |
| `translation_en` | string | no | English translation, if the source provides or implies one (e.g. parallel corpora). |
| `source` | string | yes | Short source identifier, e.g. `nllb-seed`, `community-submission`, `inpage-conversion-<batch>`. |
| `source_url` | string | no | Where the original text came from, if publicly citable. |
| `license` | string | yes | License of *this specific entry's source* — may differ from the overall corpus license if mixed sources are included. |
| `dialect_region` | string | no | If known, e.g. `srinagar`, `kupwara`. Leave null rather than guessing. |
| `domain` | string | no | Free text or controlled vocabulary, e.g. `news`, `literature`, `conversational`, `religious`, `speech-transcript`. |
| `quality_flag` | enum | yes | `native-authored`, `professionally-translated`, `mt-derived`, `community-submitted-unverified`. Critical for downstream users to filter by trust level. |
| `contributor_consent` | bool | conditional | Required (`true`) for any community-submitted entry; not applicable to entries from already-licensed public sources. |
| `date_added` | date | yes | ISO 8601, when the entry entered the corpus (not necessarily when the text was originally authored). |
| `notes` | string | no | Free-text field for anything that doesn't fit elsewhere — flag known issues here rather than silently dropping them. |

## Design principles behind this schema

- **Never force a script conversion at ingestion.** Store `script` as
  metadata and keep `text` faithful to the original. Transliteration is a
  derived, optional convenience field — going the other direction (recovering
  lost script information) isn't possible.
- **`quality_flag` exists because not all "Kashmiri text" in circulation is
  equal.** MT-derived text (e.g. Bing-translated news snippets) has already
  shown up as a labeled Kashmiri dataset elsewhere. That's a legitimate
  resource for some tasks, but it must never be silently blended with
  native-authored text without a way to tell them apart.
- **`license` is per-entry, not just per-release**, because the corpus will
  likely mix sources with different upstream terms (see `DATA_LICENSE.md`).
  This is what makes an honest overall corpus license possible.
- **`contributor_consent` exists for accountability.** If native speakers
  submit text directly, there needs to be an explicit, auditable record that
  they agreed to release it under the corpus's terms.

## Open questions (resolve before v0.1 freeze)

- Do we need a `verified_by` field for entries native speakers have
  reviewed, separate from `quality_flag`?
- Do we split into multiple files by `domain` or `quality_flag`, or keep one
  flat file and let users filter? (Recommendation: one flat file for v0.1 —
  splitting can happen later without breaking anything, but merging split
  files back together if the split was wrong is more painful.)
- Minimum viable metadata for v0.1: `id`, `text`, `script`, `source`,
  `license`, `quality_flag`, `date_added` should be non-negotiable even if
  everything else is sparse early on.
