# Desk-rejection test kit

Every test has an ID, a procedure, a pass line and its source. Run them in order: A, S, N, M, C, L, T. A desk decision is made from the front matter, so sections A and S carry the most weight.

Why scope and novelty dominate: publishers list scope and insufficient advance first, and a study of six Elsevier computer-science journals found that "many papers are rejected from the desk merely because they are a misfit to the scope of the journal" (Ghosal et al., JCDL 2019, https://impact.ornl.gov/en/publications/is-the-paper-within-scope-are-you-fishing-in-the-right-pond/). In a study of 898 rejection reports from one journal, 627 were desk rejections; of those, 46.3% cited novelty and 17.4% scope, with a median of 3 days to decision (Menon et al. 2020, https://pmc.ncbi.nlm.nih.gov/articles/PMC9022928).

---

## A. Front matter: what the editor reads

**A1. Desk simulation.** A separate reader is given only the title, abstract, contribution list and cover letter, and says what is new, which journal the paper is for, and whether it would go to review. *Pass:* they name the authors' contribution and a venue like the target, unprompted. *Source:* SOSP chairs "quickly agreed on the disposition of over 80% of the papers" (Levin & Redell, https://www.usenix.org/event/samples/submit/advice.html).

**A2. One-minute test.** State what the paper does and what is new in at most two sentences without jargon, from the paper's own words. *Pass:* one single idea, and the same one in the title, abstract and contribution list. *Source:* "Articulate your objectives using absolutely no jargon" (Heilmeier, https://www.darpa.mil/work-with-us/heilmeier-catechism); "just one 'ping': one clear, sharp idea" (Peyton Jones, https://www.microsoft.com/en-us/research/wp-content/uploads/2016/07/How-to-write-a-great-research-paper.pdf).

**A3. Title test.** Delete "novel", "efficient", "framework", "architecture", "approach" and "towards". *Pass:* what is left names the mechanism or the result, not only the area. *Fail example:* "A Novel Efficient Framework for Container Orchestration". *Source:* "The title is the ultimate refinement of the paper's contribution" (Mensh & Kording, https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1005619); Schulzrinne, https://www.cs.columbia.edu/~hgs/etc/writing-style.html.

**A4. Abstract test.** Number the sentences and label each one: problem, contribution, result or implication. *Pass:* sentence 1 or 2 states the contribution with an active verb ("We show", "We build", "We measure", "We prove"), not "This paper investigates"; results are numbers; there is no background beyond one sentence and no references. *Source:* "Put the result there, in numbers" (Koopman, https://users.ece.cmu.edu/~koopman/essays/abstract.html); "Include little if any background and motivation" (Widom, https://www.site.uottawa.ca/~bochmann/Projects/how-to-do-good-research/how-to-write-paper/Tips%20for%20Writing%20Technical%20Papers.htm). Kent Beck's four-sentence abstract puts the "startling sentence" third (https://plg.uwaterloo.ca/~migod/research/beckOOPSLA.html): merge his first two so the contribution still lands by sentence two.

**A5. Contribution-list test.** The introduction has a bulleted contribution list. *Pass:* at most three or four bullets; each is a claim that could be shown false, with a forward reference to the section that supports it; the evaluation, the dataset or "extensive experiments" are not listed as contributions unless they are the paper's point. *Fail:* "We propose X", "We study Y", or a claim with no matching experiment. *Source:* "Contributions should be refutable" (Peyton Jones); benchmarking crime E1, "not all contributions evaluated" (van der Kouwe et al., https://arxiv.org/abs/1801.02381).

**A6. Introduction test.** *Pass:* it answers, in order, what the problem is, why it matters, why it is hard, why it has not been solved, and what the key idea and results are; it ends with the contributions and evaluation claims within about 1.5 pages; no related-work survey comes before the idea. *Source:* Widom, "Why hasn't it been solved before?"; NSDI's prescreen checks that "the introduction articulates its intellectual contributions and evaluative claims" (https://www.usenix.org/conference/nsdi27/call-for-papers).

**A7. Conclusion test.** Put it beside the abstract. *Pass:* no sentence repeated; it says how the gap was filled, the limitations and how general the lessons are; it makes no claim beyond the evidence. *Source:* "under no circumstances should the paragraph simply repeat material from the Abstract or Introduction" (Widom).

**A8. Figure test.** Read each figure with only its caption. *Pass:* axes have units, absolute values appear beside ratios, variance is shown, and figures are vector or above 300 dpi. *Source:* "A figure should stand on its own" (Ernst, https://homes.cs.washington.edu/~mernst/advice/write-technical-paper.html); IEEE ">300dpi" (https://journals.ieeeauthorcenter.ieee.org/create-your-ieee-journal-article/create-graphics-for-your-article/resolution-and-size/).

---

## S. Scope: does this journal grade this kind of contribution?

A past paper on the same topic shows the topic was in scope then, under that editor, at that bar and by that route. Each test below checks one of those.

**S1. Scope sentence.** Quote the sentence on the venue's live scope page that describes the paper's main contribution, not only its setting or motivation. *Pass:* such a sentence exists and the cover letter quotes it. *Fail:* the paper appears only as a side theme (a scheduling paper at a networking journal), or no sentence names it.

**S2. Core field, not setting.** Name the primary field of each contribution and compare it with the venue's core field. *Pass:* the main contribution is in the core field. *Source:* IEEE TWC calls papers out of scope if "not centered around a wireless communications problem", naming "mobile edge computing and federated learning without considering the wireless physical layer" (https://www.comsoc.org/publications/journals/ieee-twc/policies-guidelines); NDSS excludes "Papers without any security or privacy contribution; e.g. optimizing network performance" (https://www.ndss-symposium.org/ndss2027/submissions/call-for-papers/); IEEE S&P: "Papers without a clear application to security or privacy, however, will be considered out of scope" (https://sp2026.ieee-security.org/cfpapers.html).

**S3. Kind of contribution.** Name the kind of advance: new theory, algorithm, system design, empirical finding, measurement study, deployment experience or survey. Read five recent papers in the venue and name theirs. *Pass:* the venue publishes this kind, not only this topic. A practice or experience paper sent to an algorithm-grading journal is a common cause of "limited novelty".

**S4. Explicit exclusions and moratoria.** Search the scope page and guide for authors for "not", "exclude", "out of scope", "moratorium" and "will not be considered". *Pass:* none apply. *Example:* Computers & Security: "As of early 2024, we have instituted a moratorium" on submissions with AI or ML as a significant component, including "applying an AI/ML technique to system security and privacy topics" (https://shop.elsevier.com/journals/computers-and-security/0167-4048); IEEE TDSC treats "generic systems-management problems" as out of scope (https://www.computer.org/digital-library/journals/tq/cfp-dependable-secure-computing).

**S5. Recent precedent.** Find two or three close papers in the venue from the last two to three years. Note for each whether it was a regular or a special issue, and whether the editor-in-chief or the scope text has changed since. *Pass:* recent regular-issue precedent exists. *Source:* scope statements are revised by new editors "to reflect these areas of interest and 'hot topics'" (Bader, TPDS, https://davidbader.net/publication/2017-badb/2017-badb.pdf); bars rise with submissions: IEEE TWC acceptance fell from 46.9% in 2008 to 18.3% in 2010 (Xiao, https://www.lehigh.edu/~xiaoc/Xiao_Outgoing_Editorial.pdf); a special-issue call sets its own "topics, scope, and related keywords" (https://www.elsevier.com/authors/submit-your-paper/special-issues).

**S6. Engagement with the venue's literature.** *Pass:* the paper cites and positions itself against recent, genuinely relevant papers from the venue's community. Never pad citations. *Source:* "a paper with few or no citations to recent signal processing publications is a good suspect" (IEEE SPS editor guidelines, https://signalprocessingsociety.org/publications-resources/guidelines-senior-area-editors).

**S7. Framing words.** Read the title, the first ten words of the abstract and the keywords as a classifier would. Which community do they file the paper with? *Pass:* the target venue's. *Source:* the abstract is "used to steer to the right reviewers" (Heiser, https://gernot-heiser.org/talk-howto-paper.pdf). A broad or fashionable word in the title (for example "distributed", "framework" or the name of an ML technique) can pull a paper into a different reviewer pool than intended.

**S8. Scope letters are often novelty letters.** If the paper was rejected elsewhere as out of scope, run section N as well. *Source:* Taylor & Francis's "Reject – Unsuitable" covers papers that "do not meet the editorial threshold of your journal or are out of scope" (https://editorresources.taylorandfrancis.com/welcome-to-tf/how-to/submission-portal/submission-portal-and-transfers-faqs/); "Many of our papers that we reject as under threshold are in perfect scope for another journal" (Springer Nature Transfer Desk, https://www.springernature.com/de/editors/resources-tools/transfer-desk).

**S9. Presubmission enquiry.** If S1–S5 leave doubt, recommend a short enquiry to the editor before submitting. *Source:* "Many journals have a presubmission enquiry system available—use it" (Bourne, https://pmc.ncbi.nlm.nih.gov/articles/PMC1274296/).

---

## N. Novelty: is the delta visible?

At the desk, "limited novelty" means the editor could not see a delta over the closest work in the abstract and introduction. The work may still be new.

**N1. Delta sentences.** For the three closest papers, write: "They do X; we do Y; this matters because Z." *Pass:* each Y is a mechanism or result the prior work lacks, and the paper states it in the introduction. *Fail:* Y is only a new setting or a new combination. *Source:* "something new, potentially useful, and not entirely obvious" (USENIX Security guidelines, https://static.usenix.org/events/sec01/cfp/guidelines.html); "Clearly articulate the advances beyond previous work" (OSDI '26, https://www.usenix.org/conference/osdi26/call-for-papers).

**N2. A plus B.** *Fail:* the contribution is "a straightforward combination of theories and algorithms that are well established" applied "on a known scenario" (IEEE TMBMC, https://www.comsoc.org/publications/journals/ieee-tmbmc/policies-guidelines), or there is "no new theory, algorithms, or experimental data" (IEEE SPS).

**N3. Known method, new context.** *Fail:* the paper applies an established method to a new domain without a new insight. *Source:* "Undertaking a study in a different context is not an automatic contribution" (Galvin, https://www.cambridge.org/core/services/aop-cambridge-core/content/view/3FEB4C0DA9F497B3E42B460D6A633AB8/S1833367214000698a.pdf/the-view-from-the-other-side-of-the-desk.pdf).

**N4. The platform already does it.** For systems built on a platform (Kubernetes, a cloud provider, a database, a framework), list the built-in mechanisms that express the same property. For Kubernetes placement: nodeAffinity, nodeSelector, taints and tolerations, topology spread constraints, Scheduler Framework filter and score plugins, admission controllers such as OPA Gatekeeper and Kyverno, and multi-cluster propagation policies such as Karmada's. *Pass:* the paper names them and shows a capability they cannot express, or frames the contribution as a measured result.

**N5. "First" claims.** Search for the property, not the paper's keywords, going back about 15 years, in neighbouring settings too (VMs, grids and clouds before containers). *Pass:* no "first" claim, or one narrowed to the exact delta and supported. *Source:* "Provide clear citations to work when claims of novelty are raised" (NDSS '27).

**N6. Off-the-shelf assembly.** *Fail:* the system is assembled from existing tools and the paper presents the assembly as the contribution. *Pass:* the insight, design principle or measurement is the contribution, and the parts are named as parts.

**N7. Crowded topic phrase.** Search the headline phrase. *Pass:* if it returns hundreds of papers, the abstract leads with the specific finding, not the topic.

**N8. Weakest contribution.** Reviewers score the weakest bullet. *Pass:* each bullet would survive alone; weaker ones are merged or dropped.

**N9. Obvious result.** *Fail:* a competent practitioner would have done it anyway. *Source:* "if lots of people have done the same thing, and you are simply the first person to have considered writing a paper about it, perhaps it's too obvious" (USENIX Security guidelines).

**N10. Journal version of a conference paper.** *Pass:* the paper and cover letter state what is new beyond the conference version, with a rough proportion. *Source:* Leslie Lamport records a JACM desk reject "because the basic ideas had already appeared in the conference version" (https://lamport.azurewebsites.net/pubs/pubs.html).

---

## M. Methods and evaluation: could a reviewer rebuild it?

Aim for zero benchmarking crimes, or explain each one. Tier-1 systems-security papers "commit an average of five benchmarking crimes" (van der Kouwe et al.).

**M1. Plan before results.** The evaluation questions, and the tables or figures that answer them, are stated before the results.

**M2. Claim trace.** Every number in the abstract, contributions and conclusion leads to a table or figure, and from there to raw data or scripts, using the same statistic on both sides. *Fail:* a mean compared with a median, a number found nowhere in the results, or rounding that changes the claim.

**M3. Baselines run, not copied.** Every baseline was run by the authors on matched hardware and configuration. *Fail:* comparing against numbers taken from another paper's different hardware. Also fail if the only baselines are the platform default and the authors' own variants when published or open-source alternatives exist (van der Kouwe D1–D2; Heiser, "No proper baseline", https://gernot-heiser.org/benchmarking-crimes.html).

**M4. Setup in full.** Hardware, software and versions, configurations, workloads, number of runs and their spread.

**M5. Crimes audit.** No unexplained benchmark subsets, variance shown, no arithmetic mean of normalised values, memory as well as time, absolute numbers beside relative ones. *Source:* "you only evaluate the scenarios where your approach is beneficial, you are being deceptive" (Heiser).

**M6. Assumptions perturbed.** *Pass:* assumptions are listed and their sensitivity shown. *Source:* "How sensitive is the work to perturbations of these assumptions?" (Levin & Redell, https://www.usenix.org/conferences/author-resources/how-and-how-not-write-good-systems-paper).

**M7. Where it loses.** *Pass:* the paper reports cases where the approach does worse, and the cost of every shortcut (for example, quality given up for speed).

**M8. Simulation checked.** *Pass:* simulated results are validated against at least one real run, and the simulator's assumptions are stated. *Source:* "a simulation is always a model, and contains a set of assumptions" (Heiser); network models "might produce results that are off by an order of magnitude" (Beránek et al., https://arxiv.org/abs/2204.07211).

**M9. Artifact.** *Pass:* a public repository with a pinned commit, a README, a license and "The exact commands to run to reproduce each claim from the paper" (EuroSys badges, https://sysartifacts.github.io/eurosys2025/badges). No credentials in code or history.

### Cloud, Kubernetes and scheduling papers

**M10. Scale.** Node and pod counts are stated against Kubernetes' limits of 5,000 nodes and 150,000 pods (https://kubernetes.io/docs/setup/best-practices/cluster-large/). A small real testbed is paired with a large emulated run (for example KWOK, https://kwok.sigs.k8s.io/).

**M11. Workloads.** At least one public production trace, ideally two: Google ClusterData2019 (https://github.com/google/cluster-data) and Alibaba (https://github.com/alibaba/clusterdata). Relying on one source "is leading researchers to overfit their work" (Amvrosiadis et al., https://www.usenix.org/conference/atc18/presentation/amvrosiadis).

**M12. Scheduler overhead.** The scheduler's own latency, throughput, CPU and memory are reported. Kubernetes' in-tree harness is scheduler_perf (https://github.com/kubernetes/kubernetes/blob/master/test/integration/scheduler_perf/README.md).

### Security and privacy papers

**M13. Threat model.** Attacker, capabilities, what is trusted and what is out of scope come before the design, and each claim maps to them. An adaptive attacker is tested. *Source:* USENIX Security '26 (https://www.usenix.org/conference/usenixsecurity26/call-for-papers).

**M14. ML-in-security pitfalls.** Check the ten pitfalls: sampling bias, label inaccuracy, data snooping, spurious correlations, biased parameter selection, inappropriate baseline, inappropriate measures, base-rate fallacy, lab-only evaluation and inappropriate threat model (Arp et al., https://dodo-mlsec.org/). Parameters are fixed before the test set is used.

**M15. Expected datasets and baselines.** The datasets and baselines the community expects for this genre are used, or their absence is justified.

**M16. Compliance models.** A model of a regulation (for example GDPR, HIPAA or CCPA) matches the regulation's text, and violations are measured, not assumed.

**M17. Ethics.** An ethics statement where the venue asks for one: "papers may be desk rejected for missing or inadequate ethics statements" (USENIX Security '26). An SoK must give new systematisation: "Survey papers without such insights are not appropriate and may be rejected without full review" (IEEE S&P '26).

---

## C. Compliance: every required piece

**C1. Declarations.** Data and code availability, funding, competing interests, author contributions (CRediT where asked), and ethics approval where people or their data are involved.

**C2. AI-use statement in the publisher's place.** Elsevier: a standalone section, "Declaration of generative AI and AI-assisted technologies in the manuscript preparation process", immediately before the references; no AI-created or AI-altered images of experimental data (https://www.elsevier.com/about/policies-and-standards/generative-ai-policies-for-journals). IEEE: in the acknowledgments, naming the AI system, the sections and the level of use; grammar-only use is recommended for disclosure, not required (https://open.ieee.org/author-guidelines-for-artificial-intelligence-ai-generated-text/). For ACM, Springer and others, check the live policy page.

**C3. Length counted the journal's way.** Pages in the journal's own template at its own margins, or words if the limit is in words. *Fail:* reduced margins, fonts or spacing, or core material moved to a supplement to fit the limit.

**C4. Template hygiene.** The journal's own template; no sample text, placeholders, "??" references, overfull lines in the margin or duplicated paragraphs. Some venues reject over-length papers without review: "Papers that are over the allowed number of pages will be rejected without review" (IEEE S&P '26).

**C5. Package.** Every uploaded file belongs to this paper and opens. The system-generated PDF is read end to end before approving.

**C6. Exclusive submission.** The paper is not under consideration anywhere else. A withdrawal counts once the other system shows it as withdrawn.

**C7. References.** Every reference resolves to a real DOI or URL and supports what it is cited for.

**C8. Author details.** The corresponding author uses an institutional email where the venue or its open-access agreement requires one.

---

## L. Cover letter and suggested reviewers

**L1. Show fit, don't assert it.** *Pass:* the letter quotes the scope sentence from S1, names two or three recent papers from the venue and says how this paper sits next to them. *Fail:* "This paper falls within the scope of your journal" with no evidence. *Source:* "You may understand exactly why your work is novel and different from previous work, but don't assume everybody else will" (Hamnett, https://www.timeshighereducation.com/node/595588).

**L2. State the contribution and its kind.** The first paragraph names the kind of paper (research, systems, experience, survey) and the main finding in one sentence, consistent with A2.

**L3. Disclose overlap.** Preprints, conference versions, companion papers and, where the venue asks, earlier submissions of the same work. *Source:* IEEE TWC: "Papers that do not disclose the connection to a previously rejected paper will be rejected without review" (policies page above).

**L4. Suggested reviewers.** Recent, active researchers in the venue's community, with no conflicts of interest (co-authors, same institution, close collaborators), and not only names from the reference list.

---

## T. Tier: is this the right bar for this paper now?

**T1. Kind of advance against the bar.** A new idea for a broad field, a solid contribution to a specialist field, or a design-and-experience report. Match it to venues that grade that kind (S3).

**T2. Surprise test.** If a desk reject tomorrow would not surprise the authors, aim one tier lower now.

**T3. Stopping rule.** Before submitting, name the next venue and what will change for it. If only the template changes, the next submission is likely to fail the same way.

**T4. Change before resubmitting.** After any desk reject, the title, abstract, contribution list and cover letter are rewritten to answer the stated reason, and A1 is run again. A "revise and resubmit as new" is a fresh submission that can be desk-rejected: resubmit once the requested experiments exist, with the response letter attached.

**T5. One-attempt venues.** Some venues bar a rejected paper for a period or do not reconsider it. Spend those on the strongest version.

**T6. Appeals and transfers.** Appeal only a factual misreading. Accept a transfer offer only if the new venue passes section S on its own.

*Encouragement, with evidence:* rejection is normal at every level. Leslie Lamport's Paxos paper took from 1990 to 1998, partly because readers "got so distracted by the Greek parable that they didn't understand the algorithm" (https://lamport.azurewebsites.net/pubs/pubs.html). Sally Floyd's SIGCOMM-rejected paper later won the 1999 Bennett Prize (https://www.icir.org/floyd/rejected_question.html). Re-aim the paper; don't discard it.
