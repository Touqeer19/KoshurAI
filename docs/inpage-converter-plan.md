# InPage-to-Unicode Converter — Build Plan (draft)

## Goal
Recover Kashmiri text trapped in legacy InPage-formatted documents (old
literature, newspapers, magazines) into clean Unicode text usable in
KoshurCorpus.

## Why build rather than reuse Malik's tool directly
Malik's converter (described in his 2024 paper, CC BY 4.0) reports ~98.6%
accuracy for Kashmiri specifically, but the tool itself does not appear to
be publicly released — only the resulting datasets (KS-LIT-3M, KS-PRET-5M)
are. Outreach is in progress to ask directly; in the meantime, building our
own is a viable and *not* from-scratch path, because the hard part — parsing
InPage's proprietary binary format — is already open-sourced for the shared
Perso-Arabic InPage format family that Urdu and Kashmiri both use.

## Existing open-source base to build on
- **`ltrc/inPageToUnicode`** (GitHub, LTRC / IIIT Hyderabad) — explicitly
  scoped to Perso-Arabic scripts generally, not just Urdu. Best starting
  point given the institutional/research background.
- Also available for reference/comparison: `UmerCodez/unicode-inpage-converter`,
  `zanysoft/unicode-inpage-converter` (PHP), `KamalAbdali/InpageToUnicode`
  (C, cross-platform CLI), `HassamChundrigar/InpageToUnicode`.
- All of these solve InPage binary parsing and glyph reconstruction — the
  genuinely hard reverse-engineering work — for the shared file format.

## What's actually novel work for us
The existing tools are built for Urdu's character set. Kashmiri has letters
and diacritics Urdu doesn't use, which is exactly what generic converters
get wrong (per Malik's paper's stated motivation for building a
Kashmiri-specific tool). Our real scope of work:

1. **Study the base tool's character mapping table** (likely a lookup
   table mapping InPage glyph codes to Unicode codepoints) to understand
   its structure.
2. **Build a Kashmiri-specific mapping table** — covering Kashmiri letters
   and diacritics absent from or handled differently than Urdu. This step
   needs native-speaker/linguist input, not just engineering — mapping
   errors here are what actually degrade text quality.
3. **Test against real Kashmiri InPage documents** — need sample InPage
   files written in Kashmiri to validate against. Sourcing these is itself
   a task (old newspaper archives, personal document collections, etc.).
4. **Iteratively fix mapping errors** found in testing.
5. **Optional: dictionary-based post-processing** (per Malik's approach)
   to catch/correct rare or archaic word-forms the mapping table alone
   gets wrong.

## Open questions
- Which base tool is easiest to fork/extend — needs a short technical
  evaluation (language, code quality, how the mapping table is structured)
  before committing.
- Where do we source sample Kashmiri InPage files for testing? This may be
  a bigger bottleneck than the code itself.
- Should we still wait on Malik's response before starting, in case code
  or a mapping table is shared directly? (Recommendation: start the base
  tool evaluation in parallel — it's useful either way, since even if
  Malik shares his tool, understanding the open-source alternatives is low
  -cost and non-wasted effort.)

## Status
Not started. This doc replaces the vaguer "read the paper, write a
converter" framing on issue #4 with a concrete build plan.
