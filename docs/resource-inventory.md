# Resource Inventory — Existing Kashmiri Language Resources

Living document. Update as new sources are found or evaluated. Goal: know
what already exists before duplicating effort, and track exactly what can
legally go into KoshurCorpus.

Status legend: `not reviewed` / `reviewing` / `approved for ingestion` /
`rejected` (with reason).

---

## Parallel / translation corpora

### NLLB-Seed (Meta AI) — APPROVED
- **Content:** Small human-translated parallel corpus, Wikipedia-sourced.
  Kashmiri is one of the covered languages.
- **License:** ODC-BY (Open Data Commons Attribution License), confirmed via
  official Hugging Face dataset cards (allenai/nllb, lhoestq/nllb,
  slone/nllb-200-10M-sample). Note: this corrects an earlier assumption of
  CC BY-SA — it's ODC-BY.
- **Caveat:** dataset terms also state usage is "bound to the respective
  Terms of Use and License of the original source" — since sentences trace
  back to Wikipedia, Wikipedia's CC BY-SA may still apply at the source
  level even though the packaged dataset is ODC-BY. Not a blocker, but
  worth a closer read before final ingestion.
- **Status: approved for ingestion.**

### BPCC — Bharat Parallel Corpus Collection (AI4Bharat) — APPROVED, mixed license
- **Content:** Kashmiri-English parallel corpus, part of AI4Bharat's
  broader Indic corpus collection (indicnlp_catalog / IndicTrans2).
- **License:** split by sub-collection, confirmed via AI4Bharat's IndicTrans2
  documentation:
  - BPCC-Mined, existing seed corpora (NLLB-Seed/ILCI/MASSIVE), BPCC-BT
    (back-translation): **CC0** ("no rights reserved").
  - BPCC-Human newly-added seed data (Wiki + Daily subsets) and the IN22
    test set: **CC BY 4.0**.
- **Status: approved for ingestion.** Track per-subset license in the
  `license` schema field rather than a single "BPCC" label, since CC0 and
  CC BY 4.0 carry different attribution obligations.

### NLLB-200 mined data (Meta AI)
- **Content:** Larger, automatically-mined parallel data including Kashmiri.
  Lower confidence quality than NLLB-Seed since it's mined, not
  human-translated.
- **License:** ODC-BY (same family as NLLB-Seed, confirmed via HF dataset
  cards).
- **Status:** approved for ingestion — flag as `mt-derived`/mined quality
  per our `quality_flag` schema field, since mining quality is lower than
  human-translated seed data.

---

## Monolingual text corpora

### KS-LIT-3M — REVIEWING
- **Content:** 3.1 million words (16.4M characters) of Kashmiri literary
  text, built for LM pretraining. Notable for including a converter from
  the proprietary InPage desktop-publishing format to Unicode — directly
  relevant to our own `tools/` InPage converter work.
- **License:** paper states the dataset is released "under an open
  license" but the exact license (MIT/CC-BY/ODC-BY/etc.) hasn't been
  confirmed from the paper's licensing section yet.
- **Source:** arXiv 2601.01091, Jan 2026.
- **Status: reviewing** — pull the exact license line from the paper before
  moving to approved. High priority given relevance to InPage work.

### EMILLE monolingual corpus
- **Content:** Older monolingual Kashmiri corpus from the EMILLE project.
- **License:** unclear — EMILLE corpora historically had mixed
  licensing/access terms depending on component. Needs explicit checking.
- **Status:** not reviewed.

---

## Lexical resources

### Kashmiri Wordnet
- **Content:** Lexical database (synsets, word relations).
- **License:** check terms — Wordnets are often available for research use
  but with specific attribution/redistribution conditions.
- **Status:** not reviewed. Useful for lexical coverage checks, not
  directly a text corpus source.

### Kashmiri-English dictionaries (various)
- **Content:** A few dictionaries exist; specific ones not yet catalogued.
- **Status:** not reviewed — needs a dedicated pass to identify which
  specific dictionaries exist and their terms.

---

## Speech / ASR resources

### OpenSLR SLR122 — Kashmiri Data Corpus
- **Content:** Transcribed Kashmiri speech recordings from native speakers.
- **License:** OpenSLR resources are typically openly licensed — confirm
  specific terms for SLR122.
- **Status:** not reviewed. Not a near-term priority (text corpus comes
  first) but relevant if KoshurAI expands into speech/ASR later.

---

## Adjacent / lower-priority sources (proceed with caution)

### Kashmiri news classification dataset (15,036 snippets)
- **Content:** News snippets across 10 domains, created by machine-
  translating English news into Kashmiri via Bing Translate.
- **Concern:** This is **MT-derived, not native-authored** text. Useful for
  benchmarking classification tasks, but should **never** be folded into
  KoshurCorpus as general-purpose text without an explicit
  `quality_flag: mt-derived` tag.
- **Status: rejected** for general corpus inclusion; may be worth a
  clearly-separated benchmark subset later, explicitly labeled as MT-origin.

---

## Open research gaps worth tracking

- No known large-scale, high-quality **conversational/dialogue** Kashmiri
  data exists yet — likely needs community submission rather than scraping.
- Dialectal coverage across Kashmiri-speaking regions is not well
  represented in any existing resource — be explicit in the corpus
  datasheet about which region(s) are actually represented.
- No confirmed openly-licensed large monolingual corpus beyond KS-LIT-3M's
  3.1M words — still a small amount of data for a language with millions
  of speakers, and the core gap KoshurCorpus is trying to close.

---

## License implication for KoshurCorpus overall

With NLLB-Seed and NLLB-200 confirmed as ODC-BY, and most of BPCC as CC0 /
CC BY 4.0, **ODC-BY is the stronger candidate for KoshurCorpus's overall
license** — over the originally-drafted CC BY-SA 4.0. ODC-BY matches our
highest-confidence source exactly, and CC0/CC BY 4.0 content folds into an
ODC-BY umbrella without conflict. CC BY-SA's ShareAlike clause would be the
odd one out, potentially creating friction with CC0-licensed BPCC-Mined
content. See `DATA_LICENSE.md` for the updated recommendation.

## Next actions

1. Pull KS-LIT-3M's exact license from the paper; move from `reviewing` to
   `approved`/`rejected`.
2. Confirm license terms for EMILLE, Kashmiri Wordnet, dictionaries, and
   OpenSLR SLR122 — move each from `not reviewed`.
3. Reach out (or check existing docs) for KS-LIT-3M authors regarding any
   ingestion/attribution requirements beyond the stated license.
4. Once reviewed, this doc's findings feed directly into
   `KoshurCorpus/DATA_LICENSE.md`'s per-entry license tracking.
