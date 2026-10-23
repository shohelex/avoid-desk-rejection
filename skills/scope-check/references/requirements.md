# Target journal requirements sheet

Build this sheet for the target journal before running the tests. Use the journal the user named, or the journal the template names (SKILL.md step 2). Every value comes from that journal's own pages, opened in this run, in this order:

1. The journal's guide for authors (or "submission guidelines", "information for authors") for the paper's article type.
2. Its aims-and-scope page and its list of article types.
3. The template or LaTeX page that the guide links to, and the template's own documentation.
4. Publisher-wide policy pages that the guide links to (AI use, data, ethics, preprints).
5. If a page will not open: an archived copy of that same page on web.archive.org, labelled with the snapshot date.
6. Last: `venues.md`, labelled with its date.

A value that none of these give is written **not stated**, with the pages searched. Never fill a row from memory or from another journal of the same publisher; publishers' journals differ in limits, reference styles and required statements.

Then measure the manuscript against each row. Section J of `kit.md` turns the sheet into verdicts.

## Rows

| # | Requirement | Look for in the guide | Measure in the manuscript |
| --- | --- | --- | --- |
| 1 | Journal identity | Full name, print and online ISSN, publisher, editor-in-chief | Name in the template, cover letter and file names (C11, L5) |
| 2 | Aims and scope | 2–4 verbatim phrases, the topic list | Used by S1, S2 and S12 |
| 3 | Exclusions and moratoria | "not", "exclude", "out of scope", "moratorium" | Used by S4 |
| 4 | Article types | The list, and the limits for each type | The paper's type (S11) |
| 5 | Length limit | Pages or words, in which format, and what counts (references, appendices, figures) | Pages of the compiled PDF in the journal's template, or a word count of the body (J2) |
| 6 | Over-length rules | Charges, or rejection without review | Pages over the free limit |
| 7 | Title | Length cap, rules on abbreviations | Characters or words in the title |
| 8 | Abstract | Word cap or range, structured or not, citations or abbreviations allowed | Words in the abstract; its structure (J3) |
| 9 | Keywords | How many; a controlled vocabulary such as IEEE Index Terms or the ACM CCS concepts | Number and form of keywords |
| 10 | Highlights | Required or optional, when (submission or final files), count, character cap per bullet | Highlights file or block: bullets and characters per bullet, spaces included |
| 11 | Graphical abstract | Required or optional, size and format | Present or not |
| 12 | Document class and options | The template to use and the options for a submission: review or preprint mode, single or double column, line numbers, spacing, anonymous mode | The `\documentclass[…]{…}` line and the template files (J4) |
| 13 | Journal named in the template | `\journal{…}` (elsarticle, CAS), `\acmJournal{…}` (acmart), the IEEEtran `\markboth` header, or the journal in the template's front matter | Does it name the target? (J4, C11) |
| 14 | Reference style | The `.bst` or biblatex style, numbered or author-year, DOIs required, a cap on references | `\bibliographystyle{…}` or the biblatex `style=` option; reference count; DOIs present (J5) |
| 15 | Mandatory statements | Each one, with its required heading and position: competing interests, funding, data availability, code availability, author contributions (CRediT), ethics approval, consent, AI use | Each section present, with that heading, in that place (J6, C1, C2) |
| 16 | Author information | ORCID iDs, biographies and photos, affiliation format, corresponding author's email | Present in the front matter or the back matter (J6, C8) |
| 17 | Review model | Single anonymous, double anonymous or open | Anonymity of the PDF, the source and the file names (J8, C12) |
| 18 | Figures and tables | Formats, resolution, colour, caps on counts, editable tables | Figure files and their formats (J9, A8) |
| 19 | Supplementary material | Allowed or not, size cap, whether it counts toward the length | Supplement files; what they contain (J9, C3) |
| 20 | Files at first submission | Source or PDF only, separate title page, editable figures, response letter | The files in the submission folder (J10, C5) |
| 21 | Cover letter | Required or not, required contents | The letter (L1–L5) |
| 22 | Suggested reviewers | Required or not, how many, conflict rules | A list in the submission notes (L4) |
| 23 | Prior publication | Rules for extended conference papers (share of new material, title change, citing the earlier paper) and for preprints | Overlap disclosed (N10, L3) |
| 24 | Resubmission after rejection | Waiting period or a ban | The project's notes on earlier submissions (T5, V1) |
| 25 | Data and code policy | Sharing required, encouraged or not mentioned | Statement and repository (M9) |
| 26 | Open access and APC | Subscription, hybrid or fully open access; the charge | Information only (V2) |
| 27 | Speed | Days to first decision, where the journal publishes it | Information only (V2) |
| 28 | Open special issues | Calls whose topics match the paper, with deadlines | Used by S5 and V2 |

## Measuring without a shell

The check has no shell, so measure by reading:

- **Pages:** open the compiled PDF with the Read tool; it reports the page count. If there is no PDF, say so and estimate from the source, marked "estimated".
- **Words:** count the abstract's words directly. For a body word count, estimate from the source with commands and comments removed, and say "estimated". If a measure is within 5% of a limit, mark it FIX: a different counting method could push it over.
- **Characters:** count each highlight bullet's characters including spaces.
- **Class, options and style:** quote the `\documentclass`, `\journal`, `\acmJournal` and `\bibliographystyle` lines, or the biblatex options, with their `file:line`.
