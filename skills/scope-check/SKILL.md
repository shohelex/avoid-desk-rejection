---
name: scope-check
description: Runs a desk-rejection pre-submission check on a research manuscript before it goes to a journal or conference. It covers journal scope fit, novelty, the title, abstract, contribution-list and conclusion tests, methods and evaluation, compliance, the cover letter and the tier choice, and writes a pass/fix report with evidence. Use it when the user types /scope-check, asks whether a paper is ready to submit or fits a journal, or asks why a paper was desk-rejected or rejected as out of scope or for limited novelty.
argument-hint: <manuscript file or folder> [target journal name or scope-page URL]
---

# Scope check: desk-rejection pre-submission test

Run every test in `references/kit.md` against one manuscript and one target venue. Then report which tests pass and which need a fix, with evidence for each.

Arguments: `$ARGUMENTS`. The first argument is the manuscript: a `.tex`, `.pdf`, `.md` or `.docx` file, or a folder that holds one. Anything after it names the target venue, as a journal name or the URL of its scope page.

## Ground rules

- Never edit the manuscript, cover letter or any other submission file. The output is the report alone.
- Every verdict needs evidence: a short quote with its location (`file:line`, or the page and section). Without evidence, the verdict is CAN'T TELL, never PASS.
- Venue facts (scope phrases, exclusions, limits, required statements) come only from pages you opened in this run, or from `references/venues.md` labelled with the date it gives. A fact you could not verify is written as "not verified". Never invent scope text, numbers or policies.
- Judge the paper the way an editor screens it: from the title, abstract, contribution list, introduction, figures and cover letter. Report what an editor would see in the first few minutes, not what is buried later in the paper.
- Be direct. A desk reject costs the authors weeks, so a soft PASS does more harm than a clear FIX.

## Procedure

1. **Find the files.** If the first argument is a folder, find the main manuscript: the `.tex` file with `\documentclass`, otherwise the largest PDF. Note any cover letter, supplement, response letter, upload checklist and figure folder. If there is no argument, look in the current directory, then ask the user for the path. Read a PDF with the Read tool's `pages` option, or with `pdftotext` when it is available.
2. **Extract what the editor sees.** Record the title, the abstract (numbered sentence by sentence), the keywords, the contribution list, the last paragraph of the introduction, the conclusion, the figure and table captions, the declarations, the page count and template, and the cover letter.
3. **Pin down the venue.** If no venue was given, ask for one; a scope test without a venue is meaningless. Otherwise open the venue's aims-and-scope page and its guide for authors with WebFetch, and record 2–4 verbatim scope phrases, any explicit exclusions, the length limit and the required statements. If a page will not open, say so, then use `references/venues.md` if it lists the venue, marking those facts with its date. Search the venue's last 2–3 years for papers close to this one (WebSearch, or Crossref with the journal's ISSN), and note whether each came through a regular issue or a special issue.
4. **Get an outside read.** Start one subagent and give it only the title, abstract, contribution list and cover letter: not this skill, the venue research or your own opinion. Ask it, in 3–5 sentences: what is new here, which journal or community is this paper for, and would it send the paper to review at the target venue. Its answer is the desk-simulation test (A1). Compare it with what the authors say the contribution is.
5. **Run the tests.** Work through every test in `references/kit.md` in order: sections A, S, N, M, C, L and T. For each, give PASS, FIX or CAN'T TELL, the evidence, and for FIX one concrete action. Where a rewrite helps (a title, the first two abstract sentences, a contribution bullet, the cover-letter scope paragraph), write the proposed text out in full.
6. **Rank the risks.** Pick the three FIX items most likely to cause a desk reject at this venue, in order. Scope and novelty items that an editor sees in the abstract outrank everything else.
7. **Write the report.** Save it beside the manuscript as `SCOPE_CHECK_<venue>_<YYYY-MM-DD>.md`, using `references/report-template.md`. In chat, give the verdict, the top three fixes and the report's full path, in under 15 lines.

## Verdicts

- **Ready to submit:** no FIX in sections A, S or C, and at most minor FIX items elsewhere.
- **Fix first:** one or more FIX items in sections A, N, M, C or L, at a venue that fits.
- **Wrong venue:** S1 or S3 fails. Name up to three venues whose scope text does name the paper's main contribution, and say that each must be checked the same way before submission.
