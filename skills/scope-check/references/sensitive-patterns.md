# Sensitive files and secret formats

Two layers keep credentials out of the check.

1. **Path heuristics, enforced.** The `disallowed-tools` list in `SKILL.md` holds `Read(…)` deny rules for credential folders and credential-shaped file names: cloud and VPS CLIs (AWS, Azure, Google Cloud, Oracle, IBM, Alibaba, Tencent, DigitalOcean, Hetzner, vast.ai, Linode, Vultr, Scaleway, OVH, RunPod, Modal, OpenStack), Kubernetes, Docker, Terraform and Pulumi, Git hosts and package registries, AI services, databases, password stores, keys and certificates, `.env` files and Terraform state. Claude Code refuses those reads while the skill runs; Grep and Glob honour the same rules on a best-effort basis. Path rules use glob patterns, not regular expressions.
2. **Content regex, as a pre-scan.** A secret can sit in a file with an innocent name (`notes.md`, `config.py`). Before reading anything other than the manuscript files, run the Grep tool once per pattern group below over the project, with `output_mode: "files_with_matches"`. That returns file names only, never the matching text. Treat every file it lists as secret-bearing: do not Read it, and report it by path and pattern group only.

**Never** run these patterns with `output_mode: "content"`: that would print the secret into the conversation. Patterns are Rust regex syntax, which the Grep tool uses.

## Pattern groups

**G1. Provider token formats** (high confidence)

```
AKIA[0-9A-Z]{16}|ASIA[0-9A-Z]{16}|gh[pousr]_[A-Za-z0-9]{36,}|github_pat_[A-Za-z0-9_]{60,}|glpat-[A-Za-z0-9_-]{20,}|xox[abprs]-[A-Za-z0-9-]{10,}|sk_live_[0-9A-Za-z]{24,}|AIza[0-9A-Za-z_-]{35}|dop_v1_[a-f0-9]{64}|doo_v1_[a-f0-9]{64}|dor_v1_[a-f0-9]{64}|sk-ant-[A-Za-z0-9_-]{20,}|sk-proj-[A-Za-z0-9_-]{20,}|hf_[A-Za-z0-9]{30,}|npm_[A-Za-z0-9]{36}|pypi-AgEIcHlwaS5vcmc[A-Za-z0-9_-]{50,}|SG\.[A-Za-z0-9_-]{22}\.[A-Za-z0-9_-]{43}
```

Covers: AWS access key IDs, GitHub and GitLab tokens, Slack tokens, Stripe live keys, Google API keys, DigitalOcean tokens, Anthropic and OpenAI project keys, Hugging Face tokens, npm and PyPI tokens, SendGrid keys.

**G2. Keys, certificates and connection strings** (high confidence)

```
-----BEGIN [A-Z ]*PRIVATE KEY-----|-----BEGIN OPENSSH PRIVATE KEY-----|-----BEGIN PGP PRIVATE KEY BLOCK-----|AccountKey=[A-Za-z0-9+/=]{40,}|SharedAccessSignature=|SharedAccessKey=[A-Za-z0-9+/=]{20,}|"type":\s*"service_account"|"private_key_id":|client-key-data:|client-certificate-data:|aws_secret_access_key\s*=|[a-zA-Z][a-zA-Z0-9+.-]*://[^\s/:@]+:[^\s/:@]{3,}@
```

Covers: private keys of any kind, Azure storage and Service Bus connection strings, Google service-account key files, kubeconfig client credentials, AWS credential files, and credentials embedded in URLs (`postgres://user:password@host`).

**G3. Credential assignments** (heuristic; run only on code and config files)

Run with the Grep `glob` parameter `*.{json,yaml,yml,toml,ini,cfg,conf,properties,env,py,js,ts,go,java,rb,php,sh,ps1,tf,tfvars}`:

```
(?i)(password|passwd|pwd|secret|token|api[_-]?key|access[_-]?key|client[_-]?secret|auth[_-]?token|hcloud[_-]?token|vast[_-]?api[_-]?key|do[_-]?token)\s*[:=]\s*['"]?[^\s'"$<>{}]{8,}
```

Catches hard-coded passwords and API keys, including Hetzner and vast.ai keys, which have no fixed prefix. Expect some false positives, such as a variable named `token_count = 12345678`. Report them as "possible credential, check by hand".

## Heuristics for anything the rules miss

Even when no rule matches, do not open a file whose name or folder suggests a credential: it contains `credential`, `secret`, `token`, `password`, `passwd`, `apikey`, `api_key`, `private`, `keystore`, `kubeconfig` or `.tfstate`, or it sits in a dot-folder named after a cloud, VPS or GPU provider or a command-line tool. A manuscript never needs one. If such a file looks like part of the paper (for example `secret-sharing.tex`), read it only if it has a manuscript extension (`.tex`, `.bib`, `.md`, `.docx`, `.pdf`).

## Before writing the report

Check the report text against G1 and G2 before calling Write. After writing it, run Grep on the report file alone with G1 and G2 in `files_with_matches` mode. If it is listed, overwrite the report with each match replaced by `[REDACTED: <kind>]`.
