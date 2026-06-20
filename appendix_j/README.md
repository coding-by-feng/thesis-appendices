# Appendix J — Unresolved Target Diagnostics

This repository appendix supports the title-resolution discussion in Chapter 4. It documents the unresolved target-title records that remain after the production title-resolution cascade on the canonical 19,289-Act corpus.

The full row-level snapshot is included here as [`unresolved_targets.csv`](unresolved_targets.csv). It contains 9,784 unresolved target records derived from the final network export at `data/processed/network_final/csv_v3/unresolved_targets.csv`, with `source_title` added from the canonical Act metadata.

## Summary

The unresolved file has five columns: `source_act_id`, `source_title`, `target_title`, `relation_type`, and `confidence`. Each row is an extracted relation whose free-text target title could not be resolved to a canonical `act_id`; `source_title` names the Act from which that unresolved target was extracted.

The diagnostics below are not mutually exclusive categories. They are lightweight checks over the unresolved row set, used to make the residual interpretable without listing all 9,784 rows in the thesis PDF.

| Diagnostic group | Rows | Share of unresolved rows | Interpretation |
|---|---:|---:|---|
| Total unresolved target records | 9,784 | 100.0% | Records left after the production resolver. |
| Year-bearing titles that do not match the current canonical title set under simple thesis-style normalisation | 7,160 | 73.2% | Mostly titles that appear to refer to Acts outside the current canonical corpus, including repealed or differently named historical Acts. This is a proxy, not a manually verified repeal-status label. |
| Titles with no four-digit year | 2,285 | 23.4% | Generic or family-level references where the text names an Act family but not a specific enactment year. |
| Exact `Civil List Act` / `The Civil List Act` family cites | 141 | 1.4% | A recurring year-less family citation. |
| Exact `Constitution Act` / `The Constitution Act` family cites | 132 | 1.3% | A recurring year-less family citation. |
| Titles containing a regnal marker | 7 | 0.1% | Imperial or regnal-form citations that are not normal short-title references. |
| Exact `3 and 4 Will 4, c 41` citations | 2 | 0.0% | A concrete regnal citation example. |
| Titles with impossible or corrupted four-digit strings | 28 | 0.3% | Apparent OCR, source-text, or extraction noise; examples include `1000`-series values and one currency amount misread as a date-like token. |

## Representative Examples

| Group | Example target title | Example source Act | Note |
|---|---|---|---|
| Year-bearing title absent from the canonical title set | `Land Transfer Act, 1915` | `Napier Harbour Board Empowering and Vesting Act 1917` | Top recurring unresolved target in the current residual. |
| Year-less family citation | `Civil List Act` | `Appropriation Act 1858 No 2 Act 1858 (21 and 22 Victoriae 1858 No 64)` | The title names a family of Acts but gives no enactment year. |
| Year-less family citation | `Constitution Act` | `Chinese Immigrants Amendment Act 1907 (7 EDW VII 1907 No 79)` | The title is ambiguous without a year or jurisdiction. |
| Regnal citation | `3 and 4 Will 4, c 41` | `Judicial Committee Act 1843` | Cited in regnal chapter form rather than as a New Zealand short title. |
| Corrupted four-digit string | `Civil List Act, 1020` | `Finance (No 2) Act 1942 (6 GEO VI 1942 No 14)` | The four-digit string is outside the corpus range and should not be read as a valid Act year. |

## Use in the Thesis

The thesis should not state that every year-bearing non-match is a repealed Act. The measured claim supported by this appendix is narrower: about 73% of unresolved rows are year-bearing titles that still do not match the canonical title set under simple normalisation. Earlier audits found absent or repealed Acts to dominate this class, but the current row set also includes different official names, source-text errors, OCR noise, and other title variants.

The PDF appendix therefore links to this repository appendix rather than reproducing the full CSV.
