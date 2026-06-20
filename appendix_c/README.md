## Appendix C — NER + RE Extraction Prompt (Prompt Engineering)

The prompt was iterated during gold-standard verification. The role framing, task description, five CRITICAL rules, seven relation-type definitions, and worked output example are stable; the changed output-schema lines for the retired forms are reproduced in C.1 and C.2, and C.3 reproduces the current production prompt in full.

### C.1 v1 (retired) — output-schema block

```
- "quote"       : the shortest verbatim substring from the text that
                  evidences this relation (must appear word-for-word in
                  the text above)
- "span_offsets": [start, end] character offsets of the quote within
                  the full act text (0-based, end is exclusive)
```

Retired because (i) "shortest substring" produced bare Act titles that resolved to multiple locations in roughly 40% of cases, and (ii) `span_offsets` were 93.8% hallucinated under quote-level verification on the gold standard. The `span_offsets` field was removed from both the prompt and the output schema in v2.

### C.2 v2 (retired) — output-schema block

```
- "quote"       : a verbatim substring from the text that evidences this
                  relation — include the full clause or sentence so the
                  quote is unambiguous and uniquely locatable (must appear
                  word-for-word in the text above; do NOT truncate
                  mid-sentence)
```

Retired because the "full clause or sentence" instruction caused list-item spanning and ellipsis-merge quoting in legislative enumerations: 46 of 49 unmatched quotes in the v2 verification audit were correct relations attached to non-contiguous quotes that could not be string-matched against the source.

### C.3 Current production prompt

The verbatim prompt issued to Gemini 3 Flash for extraction calls is reproduced below. The template variables `{act_text}`, `{source_title}`, and `{source_year}` are substituted per Act at request time. The task line switches between "the full text of" for full-document passes and "a chunk from" for chunked passes; the full-document wording is shown below. The act text is placed *first* and all instructions follow it so that the source document and the extraction rules sit near the beginning and end of the prompt rather than in the middle, matching the positional performance pattern reported by Liu, Lin, et al. (2024) for long-context language models (see the Prompt Engineering section for the design rationale). Only `responseMimeType: application/json` is sent in `generationConfig`; no `responseSchema` is declared, because an earlier ablation showed that response-schema enforcement caused premature stops on long Acts.

```
{act_text}

---
## ROLE

You are an expert New Zealand legal analyst specialising in legislative
Named Entity Recognition (NER) and Relation Extraction (RE).

## TASK

The text above is the full text of "{source_title}" ({source_year}).

Identify every reference to another New Zealand Act in the text above and
classify the relationship between this Act and each referenced Act.
Be EXHAUSTIVE — list ALL references found in the text, including
body text, schedules, footnotes, and consolidation notes. Do NOT stop early or summarise.

## CRITICAL rules

1. ONLY extract Acts where the COMPLETE Act title appears VERBATIM in
the text above. Most New Zealand Acts are cited in the form
"[Name] Act [Year]" (e.g. "Crimes Act 1961"), but a small number of
very old Acts have no year in their title (e.g. "Air Force Act") —
these are valid if the full title appears verbatim. Think twice and
verify before including any entry.
2. Do NOT extract self-references (i.e. references to "{source_title}").
3. Do NOT invent relationships not explicitly stated in the text.
4. Every target Act title in your output MUST appear word-for-word in
the text above.
5. legislation.govt.nz consolidation notes at the end of the document (starting with
"Notes" or "1 General") are part of the text — extract ALL Act titles
found there, including the Act named in "This is a consolidation of
the [Act]".

## Relation types

- AMD — this Act modifies the target Act
- PRP — this Act repeals specific parts of the target Act
- FRP — this Act completely repeals the entire target Act
- CIT — this Act references the target Act without modifying it
  (default fallback — use ONLY when AMD, PRP, FRP, AMD_S, R_S, PR_S
  do not apply)
- AMD_S — amendment listed in a schedule
- R_S — full repeal listed in a schedule
- PR_S — partial repeal listed in a schedule

IMPORTANT: If a target Act is being amended (AMD), partially repealed
(PRP), or fully repealed (FRP), do NOT also classify the same reference
as CIT. CIT is only for references that do not modify the target Act.
For example, "In this Act, the X Act 1971 is called the principal Act"
establishes an amendment relationship (AMD), not a citation (CIT).

Try your best to identify as many Acts as possible.

## Output format

Return a JSON object with a single key "relations" containing a list of
relation objects. Each object MUST include:
- "target_act"  : the Act title VERBATIM as it appears in the text
- "relation"    : one of the 7 relation type codes above
- "rationale"   : one sentence explaining why this relation type applies
- "quote"       : a verbatim substring from the text that evidences this
                  relation — include enough surrounding context (e.g. the
                  clause or sentence containing the Act title) so the quote
                  is unambiguous and uniquely locatable. Do NOT truncate
                  mid-sentence. Do NOT span across list items or merge
                  non-contiguous text — quote only a single contiguous
                  passage. (must appear word-for-word in the text above)
- "confidence"  : float 0.0–1.0 reflecting certainty

A target Act cited in multiple places or with multiple relation types
produces multiple objects in the list (one per evidence instance).

{
  "relations": [
    {
      "target_act": "Crimes Act 1961",
      "relation": "CIT",
      "rationale": "Section 4 uses the phrase 'within the meaning of the Crimes Act 1961' to import a definition.",
      "quote": "Section 4 uses the phrase within the meaning of the Crimes Act 1961 to import a definition of serious crime.",
      "confidence": 0.97
    },
    {
      "target_act": "Resource Management Act 1991",
      "relation": "AMD",
      "rationale": "Section 12 explicitly states this Act amends the Resource Management Act 1991 by inserting a new section.",
      "quote": "The Resource Management Act 1991 is amended by inserting, after section 70, the following section.",
      "confidence": 0.98
    },
    {
      "target_act": "Resource Management Act 1991",
      "relation": "CIT",
      "rationale": "Section 3 references the Resource Management Act 1991 for a definition without modifying it.",
      "quote": "environment has the same meaning as defined in the Resource Management Act 1991.",
      "confidence": 0.95
    }
  ]
}

If no inter-Act references are found, return:
{
  "relations": []
}
```
