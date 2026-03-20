# DOC-CORTEX-CONTENT-QUALITY — README and CONTRIBUTING follow Elsevier Cortex content conventions

**Layer:** 2 (contextual)
**Categories:** documentation, readability, contribution
**Applies-to:** docs

## Principle

`README.md` and `CONTRIBUTING.md` are the two most-read files in any repository. Both must follow a consistent section structure so that readers — human and AI alike — can locate answers immediately without scanning the entire document. This checker verifies content structure, not file existence (architecture checker) and not Markdown parse quality (AI readiness checker).

This principle maps directly to the **Docs Content Quality Checker** from [agent-ready-docs](https://github.com/elsevier-centraltechnology/agent-ready-docs). Run it with:

```bash
node ./bin/agent-ready-docs.js check --checker docs-content-quality --repo-path /path/to/your/repo
```

Checks conform to [Good Docs Project](https://thegooddocsproject.dev) templates for README and CONTRIBUTING content. See the [reference](https://github.com/elsevier-centraltechnology/agent-ready-docs/blob/main/docs/reference/docs-content-quality-checker.md) and [explanation](https://github.com/elsevier-centraltechnology/agent-ready-docs/blob/main/docs/explanation/docs-content-quality-checker.md) docs for full details.

## Why it matters

An unstructured README leaves engineers and AI agents guessing what the project does. Agents infer purpose from filenames and config files and get it wrong. A CONTRIBUTING guide that omits branching strategy causes contributors to open pull requests against the wrong base; branch naming is one of the most commonly hallucinated conventions when unspecified. Without an explicit support path, agents invent Slack channels or issue flows. Without a stated licence, agents assume permissive OSS terms — a compliance risk.

## Violations to detect

These are the exact checks run by the content quality checker. A repository is non-conformant if any MUST check fails, regardless of normalised score.

**README.md checks (RH1–RH5)**

- **RH1 (MUST)** — The first non-empty line of `README.md` is not an H1 heading (pattern: `^# `)
- **RH2 (MUST)** — No non-heading, non-empty content exists between the H1 line and the first H2 heading (the introductory paragraph is missing)
- **RH3 (MUST)** — `README.md` does not contain a heading matching `/contributing/i`, or the body of that section does not contain a Markdown link whose target matches `CONTRIBUTING.md` (pattern: `[label](./CONTRIBUTING.md)` or `[label](CONTRIBUTING.md)`)
- **RH4 (MUST)** — `README.md` contains no heading matching `/support|help|get help/i`
- **RH5 (SHOULD)** — `README.md` contains no heading matching `/licen[sc]e|terms of use/i`

**CONTRIBUTING.md checks (CH1–CH4)**

- **CH1 (MUST)** — The first non-empty line of `CONTRIBUTING.md` is not an H1 heading (pattern: `^# `)
- **CH2 (MUST)** — `CONTRIBUTING.md` contains no heading matching `/branch/i`
- **CH3 (MUST)** — `CONTRIBUTING.md` contains no heading matching `/pull request|^pr\b/i`
- **CH4 (MUST)** — `CONTRIBUTING.md` contains no heading matching `/issue|bug|report/i`

## Good practice

- Open `README.md` with `# <Project Name>` followed immediately by a one-paragraph description of what the project does and who it is for
- Include a **Contributing** section in `README.md` with the link `[CONTRIBUTING.md](CONTRIBUTING.md)`
- Include a **Help** or **Support** section in `README.md` linking to the team Slack channel, issue tracker, or support email
- Add a **Licence** section in `README.md` naming the licence and linking to the `LICENSE` file
- Open `CONTRIBUTING.md` with `# Contributing to <Project Name>`
- Add a **Branching** section to `CONTRIBUTING.md` naming the default integration branch and any naming conventions for feature, fix, or release branches
- Add a **Pull Requests** section to `CONTRIBUTING.md` covering: how to open a PR, required reviewers, CI checks that must pass, and merge strategy
- Add a **Reporting Issues** or **Bugs** section to `CONTRIBUTING.md` with a link to the issue tracker and guidance on what to include in a bug report

## Sources

- Stack, Joyce. "Docs Content Quality Checker." *agent-ready-docs* reference documentation. https://github.com/elsevier-centraltechnology/agent-ready-docs/blob/main/docs/reference/docs-content-quality-checker.md (accessed 2026-03-20).
- Stack, Joyce. "Docs Content Quality Checker." *agent-ready-docs* explanation documentation. https://github.com/elsevier-centraltechnology/agent-ready-docs/blob/main/docs/explanation/docs-content-quality-checker.md (accessed 2026-03-20).
- The Good Docs Project. "Templates." https://thegooddocsproject.dev/template/ (accessed 2026-03-20).
- GitHub. "Setting guidelines for repository contributors." GitHub Docs. https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/setting-guidelines-for-repository-contributors (accessed 2026-03-20).
