# KoshurAI

Open language resources and tools for Kashmiri (کٲشُر / कॉशुर).

## Why this exists

Kashmiri is spoken by roughly 7 million people, yet has almost no usable
infrastructure for modern NLP: a Wordnet, a handful of dictionaries, scattered
entries inside larger multilingual projects (NLLB, BPCC), and a small number
of standalone corpora. Decades of Kashmiri writing remain inaccessible to any
pipeline, much of it locked in the proprietary InPage desktop-publishing
format rather than in open, machine-readable text.

**KoshurAI's first goal is not a chatbot. It's a corpus.**

Models get superseded. A clean, well-documented, well-licensed corpus stays
useful for years and can support many downstream projects — machine
translation, speech, classification, generation — not just one demo model.
If we hold a high bar for data quality, provenance, and evaluation, this
corpus should be citable, reusable research infrastructure in its own right.

## What's here

- `KoshurCorpus/` — the corpus itself: raw sources, cleaned data, schema,
  and per-source licensing/provenance records. (Large data files are hosted
  on the Hugging Face Hub, not committed directly to this repo — see the
  corpus README once published.)
- `tools/` — ingestion, cleaning, validation, and format-conversion scripts,
  including a converter for InPage-formatted legacy Kashmiri text.
- `docs/` — resource inventory, schema spec, datasheet, and design decisions.

## Status

Early stage. Currently defining architecture, orthography policy, dataset
schema, and licensing before data collection begins. See the
[Project board](../../projects) for current milestones.

## Script policy — CONFIRMED

Kashmiri is written in more than one script. KoshurCorpus is a **multi-script
corpus**: it accepts text in any script it appears in — primarily
Perso-Arabic (Nastaliq), the dominant contemporary script, along with
Devanagari (notably used by Kashmiri Pandit communities, especially in
diaspora contexts), and Sharada where it appears in historical sources.

Every entry is tagged with its source script via the `script` field (see
`docs/schema.md`). Text is never converted or normalized to a different
script at ingestion — the original form is always preserved. Transliteration
into another script is treated as an optional, derived field that can be
added later once conversion quality is trusted; it is never a substitute for
the original.

This was decided deliberately over a single-script (Perso-Arabic-only)
approach: script conversion between Perso-Arabic, Devanagari, and Sharada
isn't always lossless, and a single-script policy would have excluded
Devanagari-writing communities from the corpus by default. Multi-script
support costs more in ingestion/cleaning engineering, but keeps the corpus
representative and keeps no information one-way-destroyed.

## License

- **Code** in this repository is licensed under [MIT](LICENSE).
- **Corpus data** (once released) will carry its own license, documented per
  release in `KoshurCorpus/DATA_LICENSE.md` — see that file for the license
  governing any given data snapshot, since individual sources folded into
  the corpus may carry their own upstream license terms (e.g. CC-BY-SA
  sources retain attribution requirements).

## Contributing

Not yet open for general contribution while the architecture and schema
are being finalized. Native speaker input is especially welcome early —
open an issue or discussion if you'd like to be involved in reviewing
script handling, dialect coverage, or data quality.

## Acknowledgements

This project builds on and cites prior work including AI4Bharat's BPCC,
Meta's NLLB-Seed, Kashmiri Wordnet, the EMILLE corpus, and other published
Kashmiri NLP research. Full citations live in `docs/resource-inventory.md`.
