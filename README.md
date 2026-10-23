# avoid-desk-rejection

A Claude Code plugin that checks a research manuscript for desk-rejection risks before you submit it. Run `/scope-check` on your paper and a target journal. It returns a pass/fix report on the things the editorial office and the editor screen for in the first few minutes:

- **The journal's own rules:** aims and scope, article type, length, abstract and keyword rules, template and document class, reference style, and the mandatory and optional elements. Each is taken from the journal's own guide and measured against your manuscript.
- **Fit:** the title, abstract, introduction, contribution list, conclusion and references, each matched against the journal's scope text and against its recent papers on your topic.
- **The paper itself:** visible novelty, methods and evaluation, required statements, real and correct references, and the cover letter.
- **The choice of journal:** whether the journal's bar fits the paper, and whether another journal would be a better home.

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

Open Claude Code in your paper's project folder and type:

```
/scope-check
```

That's all. The check finds the manuscript (`.tex`, `.docx`, `.md` or PDF), its cover letter, supplement and figures. It takes the target journal from the LaTeX template (`\journal{…}`, `\acmJournal{…}`, the IEEEtran header), then from the folder the manuscript sits in (for example `paper/toit/toit_submission/` for ACM TOIT), then from the cover letter. It tells you which journal it picked and where it found it. If it can't tell which journal you mean, it asks once.

To name your preferred journal, or point at a particular manuscript, add a journal, a path, or both. A journal you name takes priority over whatever the files say:

```
/scope-check paper/tpds/main.tex
/scope-check "IEEE Transactions on Parallel and Distributed Systems"
```

If another plugin also defines `/scope-check`, use the full name `/avoid-desk-rejection:scope-check`.

The check:

1. reads the front matter the way an editor does: title, abstract, contribution list, introduction, conclusion, figures and cover letter;
2. builds the target journal's requirements sheet from its own guide for authors, scope page and template page, about 28 rows from length and abstract limits to document class, reference style and required statements, and measures your manuscript against each row;
3. pulls the journal's papers on your topic from the last three years from OpenAlex and Crossref, using a few topic keywords and never your text. It lists the ten closest, with whether you cite each and how your paper differs;
4. asks a separate agent, given only the front matter, what is new and which journal the paper is for: an outside read that is not anchored on yours;
5. runs every test in [`skills/scope-check/references/kit.md`](skills/scope-check/references/kit.md);
6. compares the target with up to five other journals. Candidates come from the venues your references cite and from where papers on your topic were published recently, among established journals only. It compares them on scope text, recent close papers, the venue's bar and the work needed to switch, then says whether to keep the target or names a better option;
7. saves `scope-check/SCOPE_CHECK_<venue>_<date>.md` in the folder you ran it from, never inside your submission package. The report holds the verdict, the venue advice, the top three fixes, the requirements table, the fit matrix, the closest recent papers, evidence for each test and proposed rewrites.

It never edits your manuscript.

## Update

```
claude plugin update avoid-desk-rejection@avoid-desk-rejection
```

Then run `/reload-plugins` in any open session.

## What it tests

| Section | What it catches |
| --- | --- |
| A. Front matter | A contribution buried below background; a title that names only the area; contributions that cannot be refuted; hype words the design cannot back |
| S. Scope | A topic that matches but a contribution type the journal does not grade; framing that files the paper with the wrong community; explicit exclusions; a very recent near-twin in the same journal; a target the paper's own references never cite; the wrong article type or a sister journal that fits better; a title, abstract or contribution list that matches no scope phrase (fit matrix); recent close papers in the journal that the paper does not cite or position against |
| J. Journal requirements | Over the length limit; an abstract over its word cap; the wrong number or kind of keywords; another publisher's template or the wrong class options; the wrong reference style; missing highlights, statements, ORCID iDs or biographies; files the journal asks for at first submission; optional elements worth adding |
| N. Novelty | No stated delta over the closest work; "first" claims; features the platform already provides; assembled off-the-shelf parts; a question led by the tool; surveys that come too early or duplicate a recent review |
| M. Methods | Benchmarking crimes; baselines copied from other papers; simulation-only results; no threat model; ML-in-security pitfalls; claims the design cannot support |
| C. Compliance | Missing declarations and AI-use statements; shrunk margins; template leftovers; stray files; hidden text aimed at AI reviewers; text and figure reuse; another journal's name or template left in; broken anonymity; errors no co-author caught; missing reporting checklists |
| R. References | Hallucinated references: DOIs or arXiv IDs that point to the wrong paper, references found in no database, wrong metadata, retracted work, citations that do not support the claim |
| L. Cover letter | Asserting fit instead of showing it; undisclosed preprints or companion papers |
| T. Tier | A venue whose bar is above the paper; resubmitting without changing what was rejected; work too preliminary for a journal |
| V. Venue options | A better-fitting journal: one whose scope text names the contribution, which publishes more on the topic for its size, and which the paper's own references already cite. Predatory journals are left out, and so are journals that already rejected the paper and bar resubmission |

Each test cites its source: editor and publisher guidance, venue calls for papers, well-known writing and evaluation guides (Heilmeier, Peyton Jones, Widom, Levin & Redell, van der Kouwe et al., Arp et al.), and talks by journal editors, including the editor-in-chief of IEEE Access and a former IEEE President, with every quote checked against the talk's transcript.

## Security

The plugin is Markdown instructions only: no hooks, no MCP servers, no scripts. While the check runs, Claude Code refuses shell and file-editing calls and reads of 142 credential paths and file patterns, in any folder on any drive: SSH and GPG keys; AWS, Azure, Google Cloud, Oracle, DigitalOcean, Hetzner, vast.ai, Linode, Vultr, RunPod and other cloud CLIs; kubeconfig, Docker, Terraform state; Git, npm and PyPI tokens; AI-service keys; database passwords and `.env` files. A regex pre-scan, in file-names-only mode, finds secrets hidden in ordinary files so they are never opened. Everything it reads, from the manuscript and cover letter to web pages, is treated as data and never as instructions. Text hidden in a paper to steer an AI is reported as a failure (test C9), not obeyed. It fetches only venue and publisher pages (or their archived copies) and bibliographic services such as DOI, Crossref and OpenAlex, never puts your manuscript text in a URL or search, and writes only its report. See [SECURITY.md](SECURITY.md) for the threat model, what is enforced and what is only instructed, and recommended settings.

## What a run costs

The reference check makes one or more web lookups per reference. The requirements sheet, the recent-paper search and the venue comparison add a few dozen more. A full run on a 25-page paper with about 70 references takes several minutes to half an hour and a fair amount of usage. Claude Code will ask before writes and fetches unless your settings pre-approve them.

## Limits

- It cannot see an editor's private priorities, such as a quota, a special issue being planned, or a new editor-in-chief's direction. Read the venue's recent issues yourself as well.
- Venue facts are only as good as the pages that opened during the run. The report lists what it could and could not verify.
- References to ordinary websites are listed for you to check by hand rather than fetched, to keep your manuscript from being steered to an outside site.
- A pass is not a promise of review. It removes the avoidable reasons for a desk reject.

## License

MIT. See [LICENSE](LICENSE).
