# DOC-CORTEX-ARCH-COMPLIANCE — Documentation repository structure satisfies Elsevier Cortex requirements

**Layer:** 2 (contextual)
**Categories:** documentation, architecture, compliance
**Applies-to:** docs

## Principle

Every documentation repository published to Elsevier Cortex must contain the minimal set of structural files that TechDocs, Backstage, and team contributors depend on. Missing any required file breaks discoverability, rendering, or the contribution workflow. Optional files strengthen integration and should be present unless there is a deliberate reason to omit them.

## Why it matters

Cortex uses TechDocs to render and index documentation. Without the required files — especially `mkdocs.yml` with the `techdocs-core` plugin — pages will not render. Without `README.md` and `CONTRIBUTING.md`, engineers landing on the repository have no orientation and no contribution path. Structural completeness is a prerequisite for all higher-quality checks.

## Violations to detect

- **A1 (MUST)** — `README.md` is absent or empty
- **A2 (MUST)** — `CONTRIBUTING.md` is absent or empty
- **B1 (MUST)** — `mkdocs.yml` is absent or empty
- **B2 (MUST)** — `mkdocs.yml` does not list `techdocs-core` under the `plugins:` key
- **C1 (SHOULD)** — `catalog-info.yaml` is absent (reduces Backstage discoverability)

## Good practice

- Keep `README.md` at the repository root with a clear one-paragraph description of the project
- Keep `CONTRIBUTING.md` at the repository root and link to it from `README.md`
- Include a minimal `mkdocs.yml` with `site_name` and the `techdocs-core` plugin even for small repositories
- Add `catalog-info.yaml` so the service is automatically registered in the Backstage software catalog

## Sources

- Spotify. "TechDocs — Getting started." Backstage documentation. https://backstage.io/docs/features/techdocs/getting-started (accessed 2026-03-20).
- Elsevier Engineering. "Cortex Documentation Standards." Internal engineering handbook, 2025.
