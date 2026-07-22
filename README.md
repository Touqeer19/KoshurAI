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

## Script policy

Kashmiri is written in more than one script — primarily Perso-Arabic
(Nastaliq) and, less commonly, Devanagari. KoshurCorpus accepts text in
either script. Every entry is tagged with its source script; we do not
force transliteration or normalize scripts away from their original form
at ingestion. See `docs/schema.md` for details.

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
