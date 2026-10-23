# avoid-desk-rejection

A Claude Code plugin that checks a research manuscript for desk-rejection risks before you submit it. Run `/scope-check` on your paper and a target journal. It returns a pass/fix report on the things editors screen for in the first few minutes: scope fit, visible novelty, the title, abstract and contribution list, methods and evaluation, required statements, the cover letter, and whether the venue's bar fits the paper.

It was built for papers in distributed systems, cloud computing, Kubernetes and scheduling, and privacy and security. Most of the tests apply to any field.

## Install

At the prompt of a Claude Code terminal session:

```
/plugin install avoid-desk-rejection --marketplace shohelex/avoid-desk-rejection
```

Answer `y` to add the marketplace, then pick a scope (user scope makes it available in every project).

From a shell:

```
claude plugin install avoid-desk-rejection --marketplace shohelex/avoid-desk-rejection
```

In the desktop app: click **+** next to the prompt box, then **Plugins**, **Add marketplace** with `shohelex/avoid-desk-rejection`, then **Add plugin**.

## Use

```
/scope-check paper/main.tex "IEEE Transactions on Parallel and Distributed Systems"
/scope-check submission/manuscript.pdf https://www.journals.elsevier.com/future-generation-computer-systems
```

If another plugin also defines `/scope-check`, use the full name `/avoid-desk-rejection:scope-check`.

The first argument is the manuscript: a `.tex`, `.pdf`, `.md` or `.docx` file, or a folder holding one, its cover letter and its figures. The rest names the target venue, as a name or the URL of its scope page.

The check:

1. reads the front matter the way an editor does: title, abstract, contribution list, introduction, conclusion, figures and cover letter;
2. opens the venue's scope page and guide for authors, and looks for recent close papers in that venue;
3. asks a separate agent, given only the front matter, what is new and which journal the paper is for: an outside read that is not anchored on yours;
4. runs every test in [`skills/scope-check/references/kit.md`](skills/scope-check/references/kit.md);
5. saves `SCOPE_CHECK_<venue>_<date>.md` beside the manuscript, with the verdict, the top three fixes, evidence for each test and proposed rewrites.

It never edits your manuscript.

## What it tests

| Section | What it catches |
| --- | --- |
| A. Front matter | A contribution buried below background; a title that names only the area; contributions that cannot be refuted |
| S. Scope | A topic that matches but a contribution type the journal does not grade; framing that files the paper with the wrong community; explicit exclusions |
| N. Novelty | No stated delta over the closest work; "first" claims; features the platform already provides; assembled off-the-shelf parts |
| M. Methods | Benchmarking crimes; baselines copied from other papers; simulation-only results; no threat model; ML-in-security pitfalls |
| C. Compliance | Missing declarations and AI-use statements; shrunk margins; template leftovers; stray files |
| L. Cover letter | Asserting fit instead of showing it; undisclosed preprints or companion papers |
| T. Tier | A venue whose bar is above the paper; resubmitting without changing what was rejected |

Each test cites its source: editor and publisher guidance, venue calls for papers, and well-known writing and evaluation guides (Heilmeier, Peyton Jones, Widom, Levin & Redell, van der Kouwe et al., Arp et al.).

## Limits

- It cannot see an editor's private priorities, such as a quota, a special issue being planned, or a new editor-in-chief's direction. Read the venue's recent issues yourself as well.
- Venue facts are only as good as the pages that opened during the run. The report lists what it could and could not verify.
- A pass is not a promise of review. It removes the avoidable reasons for a desk reject.

## License

MIT. See [LICENSE](LICENSE).
