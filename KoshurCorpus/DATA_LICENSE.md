# KoshurCorpus Data License

**Recommended default: ODC-BY** (Open Data Commons Attribution License).

Updated from an earlier CC BY-SA 4.0 recommendation — see rationale below.
Still a placeholder pending final source review, but now backed by actual
license findings rather than a guess.

## Why ODC-BY is now the recommended default

- Our two highest-confidence, highest-priority sources are licensed this
  way or compatibly with it: **NLLB-Seed and NLLB-200 are ODC-BY**, and
  **BPCC is split between CC0 (mined/seed) and CC BY 4.0 (human-translated
  Wiki/Daily subsets)** — all of which fold cleanly under an ODC-BY
  umbrella license without conflict.
- CC BY-SA's ShareAlike clause, by contrast, would create friction with
  CC0-licensed content (CC0 waives rights entirely; forcing it under
  ShareAlike terms afterward is legally muddy) and adds a "share-alike"
  obligation that most ML practitioners don't expect from training data
  licenses.
- ODC-BY is purpose-built for datasets (as opposed to CC licenses, which
  were designed primarily for creative works), and is increasingly the
  norm for ML training corpora specifically.

## What still needs to happen before this is final

1. **Finish auditing remaining sources** — KS-LIT-3M (license not yet
   confirmed), EMILLE, Kashmiri Wordnet, dictionaries, OpenSLR SLR122. See
   `docs/resource-inventory.md` for current status. A source under a more
   restrictive license (non-commercial-only, no explicit license, etc.)
   either gets excluded, kept in a separately-licensed subset, or requires
   explicit rights-holder permission — it cannot simply be relabeled ODC-BY.
2. **Track per-entry provenance and license** in the dataset schema (see
   `docs/schema.md`, `license` field) so the corpus can honestly represent
   mixed licensing — this already matters given BPCC alone spans two
   licenses internally.
3. **Decide on contributor consent terms** for any community-submitted
   text (e.g. native speakers submitting sentences via form) — contributors
   should explicitly agree to release their submission under the corpus
   license (ODC-BY) at submission time.
4. **Double-check the NLLB-Seed "bound to original source terms" clause** —
   since NLLB-Seed sentences trace back to Wikipedia (CC BY-SA at the
   source level), confirm this doesn't impose any obligation beyond what
   ODC-BY already covers before finalizing.

## Per-release licensing

Each dataset release (v0.1, v0.2, ... v1.0) should restate its license and
any exceptions in its own release notes / dataset card on Hugging Face,
even if the license doesn't change — this keeps provenance auditable
release over release, especially given the corpus mixes sources with
different underlying license histories.
