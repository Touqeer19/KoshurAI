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

### Kashmiri-English Parallel Corpus (SMUQamar, HF) — NEW, not yet reviewed
- **Content:** 30,000 sentence pairs publicly released (270,000 pairs total,
  larger set available on request). Includes raw/manual/OCR-scanned
  subsets and a cleaned version. From Qumar, Azim & Quadri (2024),
  "Addressing the data gap: building a parallel corpus for Kashmiri
  language."
- **License:** not yet confirmed — check the HF dataset card directly.
- **Status:** not reviewed — worth checking soon given it's a dedicated,
  purpose-built Kashmiri parallel corpus, not a byproduct of a larger
  multilingual project.

---

## Monolingual text corpora

### Kashmiri Wikipedia — NEW, high value
- **Content:** Native-authored Kashmiri text, actively growing (8,529+
  articles as of Dec 2025). This is **genuine native Kashmiri writing**,
  not translated or mined — valuable given how little native-authored
  monolingual text exists elsewhere in this inventory.
- **License: CC BY-SA 4.0** (most text also dual-licensed under GFDL),
  confirmed.
- **Caveat:** CC BY-SA's ShareAlike clause is the one point of friction
  with our ODC-BY recommendation — ShareAlike content can generally be
  *included* in a larger ODC-BY-licensed collection as long as the
  CC BY-SA portion itself is still clearly attributed and its own terms
  respected (i.e. don't claim the Wikipedia-derived subset is ODC-BY-only
  licensed) — but this needs a real license-compatibility check, not a
  quick assumption, before ingestion. Recommend tracking this subset's
  license explicitly as `cc-by-sa-4.0` in the `license` field rather than
  letting it get flattened to "ODC-BY" corpus-wide.
- **Status: reviewing** — high-value source, but the CC BY-SA interaction
  with the rest of the corpus needs a clear-headed check first.

### Kashmiri Raw Text Corpus / LDC-IL (CIIL) — NEW, likely restricted
- **Content:** 466,054 words, drawn from books, newspapers, and magazines
  (Aesthetics and Social Sciences domains). Published by the Central
  Institute of Indian Languages (Ramamoorthy, Choudhary & Bhat, 2019).
- **License:** not yet confirmed, but hosted via LDC-IL (Linguistic Data
  Consortium for Indian Languages) — resources distributed this way
  historically often require registration/access agreements similar to
  EMILLE's, rather than being freely redistributable. Treat with the same
  caution as EMILLE until proven otherwise.
- **Status:** not reviewed — check LDC-IL's access terms directly before
  assuming it's open.

### KS-LIT-3M — APPROVED
- **Content:** 3.1 million words (16.4M characters) of Kashmiri literary
  text, built for LM pretraining. Notable for including a converter from
  the proprietary InPage desktop-publishing format to Unicode — directly
  relevant to our own `tools/` InPage converter work.
- **License: CC BY 4.0**, confirmed — permits sharing and adaptation with
  attribution; author requests citation of the paper (Malik, arXiv
  2601.01091, 2026) when the dataset is used.
- **Source:** arXiv 2601.01091, Jan 2026. Hosted on Hugging Face under
  author Haq Nawaz Malik (huggingface.co/Omarrran).
- **Status: approved for ingestion.** CC BY 4.0 folds cleanly under our
  ODC-BY corpus license recommendation.

### KS-PRET-5M — NEW, not yet reviewed in depth
- **Content:** Follow-up/extension of KS-LIT-3M by the same author. 5.09
  million words, 12.13M subword tokens — broader genre coverage than
  KS-LIT-3M (adds journalism, biography, academic writing, religious
  scholarship) plus Unicode-native web-sourced text.
- **License:** CC BY 4.0, "with a few custom restrictions noted on the
  Hugging Face dataset card" — needs a direct read of that card before
  approving, since the exact restrictions aren't stated in the paper text
  reviewed so far.
- **Source:** arXiv 2604.11066, hosted at
  huggingface.co/datasets/Omarrran/KS-PRET-5M_5_million_kashmiri_Pretrainning_LLM_dataset_12M_tokens_2026
- **Status: reviewing** — larger and broader than KS-LIT-3M, high priority
  to check the dataset card's custom restrictions.

### 600K-KS-OCR — NEW, lower priority for now
- **Content:** ~602,000 word-level synthetic image dataset for OCR on
  Kashmiri script (not raw text — image + transcription pairs). Not
  directly usable for KoshurCorpus's text corpus, but relevant if KoshurAI
  ever needs OCR for scanned (non-InPage) Kashmiri documents.
- **License:** CC-BY-4.0, confirmed.
- **Source:** arXiv 2601.01088, same author (Malik).
- **Status:** not reviewed for inclusion — parked as a future-relevance
  note, not a text-corpus candidate right now.

### EMILLE monolingual corpus — REJECTED
- **Content:** Older monolingual Kashmiri corpus (part of a 97M-word
  multi-language South Asian corpus) from the EMILLE project
  (Lancaster University / CIIL Mysore).
- **License: restrictive, confirmed.** The EMILLE/CIIL Corpus is
  distributed free of charge for non-profit-making research only, under a
  formal End User Licence Agreement with the EMILLE Consortium — it is
  not freely redistributable, requires an executed agreement per licensee,
  includes usage-tracking/reporting obligations, and mandates deletion of
  all copies on termination. A separate "EMILLE Lancaster Corpus" variant
  exists for commercial use but under its own separate (also restrictive)
  terms.
- **Status: rejected for inclusion.** Incompatible with an openly-licensed,
  freely-redistributable corpus like KoshurCorpus. Do not ingest without
  a direct, explicit agreement from the EMILLE Consortium — and even then,
  redistribution as part of an open corpus release is unlikely to be
  permitted under these terms.

---

## Lexical resources

### Kashmiri Wordnet — REVIEWING, licensing pattern identified
- **Content:** Lexical database (synsets, word relations), part of the
  IndoWordNet project led by IIT Bombay's CFILT lab, alongside Hindi
  Wordnet and 16 other Indian language wordnets.
- **License:** not separately confirmed for Kashmiri specifically, but the
  IndoWordNet family pattern (per Hindi Wordnet, the flagship member) is
  **GNU GPL 3.0** for the API/software and **GNU FDL** (GNU Free
  Documentation License) for the lexicon data itself. GPL/FDL are not
  directly ODC-BY-compatible — GPL is a strong copyleft license for code,
  and FDL has its own (non-CC, non-ODC) share-alike-style terms for
  content. Would need explicit legal comparison before folding lexicon
  data into an ODC-BY corpus.
- **Status: reviewing** — likely lower priority anyway since this is a
  lexical resource (word-sense data), not raw corpus text; useful for
  coverage-checking rather than direct ingestion regardless of license
  resolution.

### Kashmiri-English dictionaries (various)
- **Content:** A few dictionaries exist; specific ones not yet catalogued.
- **Status:** not reviewed — needs a dedicated pass to identify which
  specific dictionaries exist and their terms.

---

## Speech / ASR resources

### OpenSLR SLR122 — Kashmiri Data Corpus — APPROVED (for future speech work)
- **Content:** Transcribed Kashmiri speech recordings and transcripts from
  native speakers, collected by a student group working on Kashmiri ASR.
  ~394MB archive.
- **License: GPL-3.0-or-later**, confirmed directly from the OpenSLR
  resource page. Note: GPL is a copyleft license, not directly the same
  family as ODC-BY/CC0/CC BY — if this is ever ingested, its GPL terms
  need to be respected explicitly for that subset rather than assumed to
  fold cleanly into the overall corpus license.
- **Status: approved for future use**, not a near-term priority (text
  corpus comes first) but relevant once KoshurAI expands into speech/ASR.
  Also found: **RASA Kashmiri Dataset** (studio-quality recordings) and
  the **Kashmiri split of IndicVoices-R** (spontaneous multi-speaker
  recordings) — both referenced in recent Kashmiri TTS research
  (arXiv 2603.07513) as additional speech sources worth a license check
  when speech work becomes relevant.

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

With NLLB-Seed, NLLB-200, and KS-LIT-3M confirmed as ODC-BY/CC BY 4.0, and
most of BPCC as CC0/CC BY 4.0, **ODC-BY remains the stronger candidate for
KoshurCorpus's overall license** over the originally-drafted CC BY-SA 4.0.
The one genuine complication found today is **Kashmiri Wikipedia**
(CC BY-SA 4.0) — a high-value native-authored source whose ShareAlike
clause doesn't fold as cleanly under ODC-BY as the other approved sources.
Recommend treating the corpus as **ODC-BY overall, with individual
CC BY-SA-sourced subsets (e.g. Wikipedia-derived text) explicitly tagged
with their own license in the `license` field** rather than forcing a
single blanket license claim across all included text — this is honest
about provenance and avoids any accidental license-washing.

**Confirmed rejection:** EMILLE is not usable — its distribution terms are
non-profit-research-only under a formal per-licensee agreement with no
redistribution rights, incompatible with an open corpus release. The
similarly CIIL-affiliated **LDC-IL Kashmiri Raw Text Corpus** should be
treated with the same suspicion until its access terms are confirmed
directly.

## Next actions

1. **Kashmiri Wikipedia**: get a definitive answer on CC BY-SA inclusion
   under an ODC-BY umbrella (likely fine with correct per-subset
   attribution, but confirm before ingesting — this is a genuinely
   valuable native-text source worth getting right rather than skipping).
2. **KS-PRET-5M**: read the actual Hugging Face dataset card for its
   "custom restrictions" before approving — it's larger and more
   diverse than KS-LIT-3M and worth prioritizing.
3. **Kashmiri-English Parallel Corpus (SMUQamar)**: check HF dataset card
   license — purpose-built Kashmiri corpus, not a byproduct of a larger
   project, worth the few minutes to confirm.
4. **LDC-IL Kashmiri Raw Text Corpus**: confirm access/redistribution
   terms directly — do not assume open given the CIIL/EMILLE-adjacent
   history.
5. **Kashmiri-English dictionaries**: still needs a dedicated pass to
   identify which specific dictionaries exist and their terms — lowest
   priority, not blocking anything else.
6. Once resolved, all findings feed directly into
   `KoshurCorpus/DATA_LICENSE.md`'s per-entry license tracking.
