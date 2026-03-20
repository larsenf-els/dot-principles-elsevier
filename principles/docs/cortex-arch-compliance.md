# DOC-CORTEX-ARCH-COMPLIANCE — Documentation repository structure satisfies Elsevier Cortex requirements

**Layer:** 2 (contextual)
**Categories:** documentation, architecture, compliance
**Applies-to:** docs

## Principle

Every documentation repository published to Elsevier Cortex must contain the minimal set of structural files that TechDocs, Backstage, and team contributors depend on. Missing any required file breaks discoverability, rendering, or the contribution workflow.

This principle maps directly to the **Docs Architecture Compliance Checker** from [agent-ready-docs](https://github.com/elsevier-centraltechnology/agent-ready-docs). Run it with:

```bash
node ./bin/agent-ready-docs.js check --checker architecture --repo-path /path/to/your/repo
```

See the [reference](https://github.com/elsevier-centraltechnology/agent-ready-docs/blob/main/docs/reference/docs-architecture-compliance-checker.md) and [explanation](https://github.com/elsevier-centraltechnology/agent-ready-docs/blob/main/docs/explanation/architecture-checks.md) docs for full details.

## Why it matters

Cortex uses TechDocs to render and index documentation. Without `mkdocs.yml` with the `techdocs-core` plugin, pages will not render — it produces a silent build failure with no error in the catalog. Without `README.md` and `CONTRIBUTING.md`, engineers and AI agents have no orientation and no contribution path; agents fall back to generic Git workflow advice that may violate the project's actual conventions.

## Violations to detect

These are the exact checks run by the architecture checker. A repository cannot be rated adherent if any MUST check fails, regardless of total score.

**A. Required Repository Documentation**

- **A1 (MUST)** — `README.md` is absent, is not a regular file, or contains only whitespace
- **A2 (MUST)** — `CONTRIBUTING.md` is absent, is not a regular file, or contains only whitespace

**B. MkDocs Configuration**

- **B1 (MUST)** — `mkdocs.yml` is absent, is not a regular file, or contains only whitespace
- **B2 (MUST)** — `mkdocs.yml` exists but its `plugins:` key does not include `techdocs-core` (either as a bare string entry or as an object key); also fails if `mkdocs.yml` cannot be parsed as YAML

**C. Backstage Publication Evidence**

- **C1 (SHOULD)** — `catalog-info.yaml` is absent at the repository root (missing reduces Backstage discoverability but does not fail MUST compliance)

## Good practice

- Keep `README.md` at the repository root with a clear one-paragraph description of the project
- Keep `CONTRIBUTING.md` at the repository root and link to it from `README.md`
- Include a minimal `mkdocs.yml` with `site_name` and the `techdocs-core` plugin even for small repositories
- Add `catalog-info.yaml` so the service is automatically registered in the Backstage software catalog

## Sources

- Spotify. "TechDocs — Getting started." Backstage documentation. https://backstage.io/docs/features/techdocs/getting-started (accessed 2026-03-20).
- Stack, Joyce. "Docs Architecture Compliance Checker." *agent-ready-docs* reference documentation. https://github.com/elsevier-centraltechnology/agent-ready-docs/blob/main/docs/reference/docs-architecture-compliance-checker.md (accessed 2026-03-20).
- Stack, Joyce. "Architecture Checks." *agent-ready-docs* explanation documentation. https://github.com/elsevier-centraltechnology/agent-ready-docs/blob/main/docs/explanation/architecture-checks.md (accessed 2026-03-20).
