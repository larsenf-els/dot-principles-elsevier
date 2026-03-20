# DOC-CORTEX-CONTENT-QUALITY — README and CONTRIBUTING follow Elsevier Cortex content conventions

**Layer:** 2 (contextual)
**Categories:** documentation, readability, contribution
**Applies-to:** docs

## Principle

`README.md` and `CONTRIBUTING.md` are the two most-read files in any repository. Readers arrive with specific questions: "What is this?", "How do I set it up?", "Where do I get help?", "How do I contribute?", "On which branch do I base my work?" Both files must follow a consistent section structure so that readers — human and AI alike — can locate answers immediately without scanning the entire document.

## Why it matters

An unstructured README leaves engineers guessing what the project does and where to begin. A CONTRIBUTING guide that omits branching strategy causes contributors to open pull requests against the wrong base, breaking CI or release workflows. Consistent structure across all Cortex repositories reduces onboarding friction and makes documentation reliably parseable by automated tools.

## Violations to detect

### README checks

- **RH1 (MUST)** — `README.md` does not open with an H1 heading (`# Project Name`)
- **RH2 (MUST)** — `README.md` has no prose content between the H1 heading and the first H2 section (the intro paragraph is missing)
- **RH3 (MUST)** — `README.md` does not contain a Contributing section that links to `CONTRIBUTING.md`
- **RH4 (MUST)** — `README.md` does not contain a Help or Support section describing where to ask questions or report issues
- **RH5 (SHOULD)** — `README.md` does not contain a Licence section identifying the project licence

### CONTRIBUTING checks

- **CH1 (MUST)** — `CONTRIBUTING.md` does not open with an H1 heading
- **CH2 (MUST)** — `CONTRIBUTING.md` does not contain a section describing the branching strategy (which branch to fork from, branch naming conventions)
- **CH3 (MUST)** — `CONTRIBUTING.md` does not contain a section describing the pull request process
- **CH4 (MUST)** — `CONTRIBUTING.md` does not contain a section for issue or bug reporting

## Good practice

- Open `README.md` with `# <Project Name>` followed immediately by a one-paragraph description of what the project does and who it is for
- Include a **Contributing** section in `README.md` with a direct link: `See [CONTRIBUTING.md](CONTRIBUTING.md)`
- Include a **Help** or **Support** section in `README.md` linking to the team Slack channel, issue tracker, or support email
- Add a **Licence** section in `README.md` naming the licence and linking to the `LICENSE` file
- Open `CONTRIBUTING.md` with `# Contributing to <Project Name>`
- Add a **Branching** section to `CONTRIBUTING.md` that names the default integration branch (e.g., `main`) and any naming conventions for feature, fix, or release branches
- Add a **Pull Requests** section to `CONTRIBUTING.md` covering: how to open a PR, required reviewers, CI checks that must pass, and merge strategy
- Add a **Reporting Issues** section to `CONTRIBUTING.md` with a link to the issue tracker and guidance on what to include in a bug report

## Sources

- GitHub. "About READMEs." GitHub Docs. https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes (accessed 2026-03-20).
- GitHub. "Setting guidelines for repository contributors." GitHub Docs. https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/setting-guidelines-for-repository-contributors (accessed 2026-03-20).
- Elsevier Engineering. "Cortex Documentation Standards." Internal engineering handbook, 2025.
