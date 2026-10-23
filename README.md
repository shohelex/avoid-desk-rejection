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

Open Claude Code in your paper's project folder and type:

```
/scope-check
```

That's all. The check finds the manuscript (`.tex`, `.docx`, `.md` or PDF), its cover letter, supplement and figures, and works out the target journal from the cover letter, the LaTeX template or the folder names. It tells you what it picked. If it can't tell which journal you mean, it asks once.

To point it somewhere specific, add a path, a journal, or both:

```
/scope-check paper/tpds/main.tex
/scope-check "IEEE Transactions on Parallel and Distributed Systems"
```

If another plugin also defines `/scope-check`, use the full name `/avoid-desk-rejection:scope-check`.

The check:

1. reads the front matter the way an editor does: title, abstract, contribution list, introduction, conclusion, figures and cover letter;
2. opens the venue's scope page and guide for authors, and looks for recent close papers in that venue;
3. asks a separate agent, given only the front matter, what is new and which journal the paper is for: an outside read that is not anchored on yours;
4. runs every test in [`skills/scope-check/references/kit.md`](skills/scope-check/references/kit.md);
5. saves `scope-check/SCOPE_CHECK_<venue>_<date>.md` in the folder you ran it from, never inside your submission package, with the verdict, the top three fixes, evidence for each test and proposed rewrites.

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
| S. Scope | A topic that matches but a contribution type the journal does not grade; framing that files the paper with the wrong community; explicit exclusions; a very recent near-twin in the same journal; a target the paper's own references never cite; the wrong article type or a sister journal that fits better |
| N. Novelty | No stated delta over the closest work; "first" claims; features the platform already provides; assembled off-the-shelf parts; a question led by the tool; surveys that come too early or duplicate a recent review |
| M. Methods | Benchmarking crimes; baselines copied from other papers; simulation-only results; no threat model; ML-in-security pitfalls; claims the design cannot support |
| C. Compliance | Missing declarations and AI-use statements; shrunk margins; template leftovers; stray files; hidden text aimed at AI reviewers; text and figure reuse; another journal's name or template left in; broken anonymity; errors no co-author caught; missing reporting checklists |
| R. References | Hallucinated references: DOIs or arXiv IDs that point to the wrong paper, references found in no database, wrong metadata, retracted work, citations that do not support the claim |
| L. Cover letter | Asserting fit instead of showing it; undisclosed preprints or companion papers |
| T. Tier | A venue whose bar is above the paper; resubmitting without changing what was rejected; work too preliminary for a journal |

Each test cites its source: editor and publisher guidance, venue calls for papers, well-known writing and evaluation guides (Heilmeier, Peyton Jones, Widom, Levin & Redell, van der Kouwe et al., Arp et al.), and talks by journal editors, including the editor-in-chief of IEEE Access and a former IEEE President, with every quote checked against the talk's transcript.

## Security

The plugin is Markdown instructions only: no hooks, no MCP servers, no scripts. While the check runs, Claude Code refuses shell and file-editing calls and reads of 142 credential paths and file patterns: SSH and GPG keys; AWS, Azure, Google Cloud, Oracle, DigitalOcean, Hetzner, vast.ai, Linode, Vultr, RunPod and other cloud CLIs; kubeconfig, Docker, Terraform state; Git, npm and PyPI tokens; AI-service keys; database passwords and `.env` files. A regex pre-scan, in file-names-only mode, finds secrets hidden in ordinary files so they are never opened. Everything it reads, from the manuscript and cover letter to web pages, is treated as data and never as instructions. Text hidden in a paper to steer an AI is reported as a failure (test C9), not obeyed. It fetches only venue, publisher and DOI pages, never puts your manuscript text in a URL or search, and writes only its report. See [SECURITY.md](SECURITY.md) for the threat model, what is enforced and what is only instructed, and recommended settings.

## What a run costs

The reference check makes one or more web lookups per reference, so a full run on a 25-page paper with about 70 references takes several minutes to half an hour and a fair amount of usage. Claude Code will ask before writes and fetches unless your settings pre-approve them.

## Limits

- It cannot see an editor's private priorities, such as a quota, a special issue being planned, or a new editor-in-chief's direction. Read the venue's recent issues yourself as well.
- Venue facts are only as good as the pages that opened during the run. The report lists what it could and could not verify.
- References to ordinary websites are listed for you to check by hand rather than fetched, to keep your manuscript from being steered to an outside site.
- A pass is not a promise of review. It removes the avoidable reasons for a desk reject.

## License

MIT. See [LICENSE](LICENSE).
