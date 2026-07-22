# KoshurCorpus Data License

**Recommended default: CC BY-SA 4.0** (Creative Commons Attribution-ShareAlike 4.0).

This is a placeholder recommendation, not a final decision — confirm before v0.1 release.

## Why CC BY-SA 4.0 is the likely default

- It's the license used by several major sources you'll likely fold in
  (e.g. NLLB-Seed's Wikipedia-derived text is CC BY-SA), and matching your
  outbound license to your most significant inbound source avoids license
  conflicts.
- ShareAlike keeps the corpus and any derivatives open — a downstream user
  can't take the corpus, improve it, and close the improved version off.
- It's a well-understood, standard choice for language corpora, which
  matters for adoption by other researchers.

## What needs to happen before this is final

1. **Audit every source going into the corpus** for its own license terms.
   A source under a more restrictive license (e.g. non-commercial-only, or
   all-rights-reserved text scraped with permission but no explicit license)
   can't simply be relicensed as CC BY-SA — it either gets excluded, kept in
   a separately-licensed subset, or requires explicit permission from the
   rights holder.
2. **Track per-entry provenance and license** in the dataset schema (see
   `docs/schema.md`, `license` field) so the corpus can honestly represent
   mixed licensing if it turns out not everything can be CC BY-SA.
3. **Decide on contributor consent terms** for any community-submitted text
   (e.g. native speakers submitting sentences via form) — contributors
   should explicitly agree to release their submission under the corpus
   license at submission time, not after the fact.
4. Consider **ODC-BY** as an alternative if CC BY-SA's ShareAlike clause
   turns out to complicate use by model trainers (some ML practitioners
   prefer ODC-BY / CC BY for data specifically, reserving CC BY-SA for
   more traditional creative works). Worth a short discussion before
   locking this in.

## Per-release licensing

Each dataset release (v0.1, v0.2, ... v1.0) should restate its license and
any exceptions in its own release notes / dataset card on Hugging Face,
even if the license doesn't change — this keeps provenance auditable
release over release.
