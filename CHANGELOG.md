cre# Changelog

All notable changes to `.principles` will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/), and this project adheres to [Semantic Versioning](https://semver.org/).

> **Note:** `.principles` is in its early days — this is an experimental release. The system is being actively used and iterated on, but expect rough edges, evolving formats, and breaking changes as things stabilize.

---

## [Unreleased]

### Added

- **4 new code smell principles** completing all 22 Fowler *Refactoring* 1st-edition smells and adding the 2 smells introduced in the 2nd edition — `CODE-SMELLS-LAZY-ELEMENT` (layer 2), `CODE-SMELLS-MIDDLE-MAN` (layer 2), `CODE-SMELLS-MUTABLE-DATA` (layer 2), `CODE-SMELLS-LOOPS` (layer 2, `Audit-scope: limited`). `code-smells` namespace expanded from 18 to 22 principles. Source: Fowler, Martin. *Refactoring: Improving the Design of Existing Code*, 2nd ed. Addison-Wesley, 2018. ISBN 978-0-13-475759-9. Chapter 3.
- **Updated `code-smells` context files** — `.context-audit.md` and `.context-prime.md` now cover all 22 code-smell principles.
- **Updated `groups/code-smells.yaml`** — all 4 new principles added (22 total).
- **Fixed missing code-smell catalog entries** — 9 existing code-smell principles (`ALTERNATIVE-CLASSES`, `DATA-CLASS`, `DIVERGENT-CHANGE`, `GLOBAL-DATA`, `INSIDER-TRADING`, `LONG-PARAMETER-LIST`, `REFUSED-BEQUEST`, `SHOTGUN-SURGERY`, `TEMPORARY-FIELD`) were present as files but had no `catalog.yaml` entries; added alongside the 4 new entries (22 code-smell entries total in catalog).

- **4 new container / Dockerfile principles** in `infra` namespace — `INFRA-NON-ROOT-CONTAINER` (layer 1, with inspection), `INFRA-PIN-BASE-IMAGES` (layer 1, with inspection), `INFRA-MINIMIZE-IMAGE-LAYERS` (layer 1, with inspection), `INFRA-NO-SECRETS-IN-IMAGE` (layer 1, with inspection). Sources: CIS Docker Benchmark v1.6.0 (Sections 4.1, 4.10, 5.1), OWASP Docker Security Cheat Sheet, Docker official Dockerfile best practices, OpenSSF SLSA v1.0, Google Distroless container images.
- **New `.context-inspect.md` for infra** — machine-executable pre-scan patterns for all 4 new container principles (7 grep patterns total).
- **Updated `infra` context files** — `.context-audit.md` and `.context-prime.md` now include all 4 new container principles.
- **Updated `layers/infra/layer-2-contexts.yaml`** — `containers` context now activates all 4 new principles in addition to the 2 existing entries.
- **Updated `groups/security-focused.yaml`** — `INFRA-NON-ROOT-CONTAINER`, `INFRA-PIN-BASE-IMAGES`, and `INFRA-NO-SECRETS-IN-IMAGE` added (43 security-focused principles total).

- **5 new Saltzer & Schroeder security architecture principles** in `sec-arch` namespace — `SEC-ARCH-ECONOMY-OF-MECHANISM` (with inspection), `SEC-ARCH-SEPARATION-OF-PRIVILEGE`, `SEC-ARCH-LEAST-COMMON-MECHANISM` (with inspection), `SEC-ARCH-PSYCHOLOGICAL-ACCEPTABILITY` (`Audit-scope: limited`), `SEC-ARCH-OPEN-DESIGN` (with inspection). Completes all 8 Saltzer & Schroeder (1975) design principles in the catalog (3 were already covered: `CODE-SEC-COMPLETE-MEDIATION`, `CODE-SEC-FAIL-SAFE-DEFAULTS`, `INFRA-LEAST-PRIVILEGE`). Source: Saltzer & Schroeder, "The Protection of Information in Computer Systems", *Proceedings of the IEEE* 63(9), 1975, DOI 10.1109/PROC.1975.9939.
- **Updated `sec-arch` context files** — `.context-audit.md` and `.context-prime.md` now cover all 8 sec-arch principles (3 existing + 5 new).
- **New `.context-inspect.md` for sec-arch** — machine-executable pre-scan patterns for 4 sec-arch principles with grep-able violations (`supply-chain-security`, `economy-of-mechanism`, `least-common-mechanism`, `open-design`).
- **Updated `groups/security-focused.yaml`** — all 5 new principles added (40 security-focused principles total).
- **3 new schema design principles** in `schema` namespace — `SCHEMA-FIELD-OPTIONALITY` (layer 1, with inspection), `SCHEMA-NO-POLYMORPHIC-BLOBS` (layer 1, with inspection), `SCHEMA-ENUM-EVOLUTION` (layer 1, with inspection). Schema namespace expanded from 1 to 4 principles. Sources: Google Protocol Buffers Language Guide (proto3), Apache Avro Specification 1.11.1, Kleppmann *Designing Data-Intensive Applications* (ISBN 978-1-449-37332-0), OpenAPI Specification 3.1.0, Google API Design Guide.
- **Updated schema layer files** — `layers/schema/layer-1-universal.md` adds 3 new layer-1 principles; `layers/schema/layer-2-contexts.yaml` activates new principles in OpenAPI, Protobuf, GraphQL, and SQL contexts; new `avro` context added.
- **New `.context-inspect.md` for schema** — machine-executable pre-scan patterns for all 3 new schema principles.
- **Updated schema context files** — `.context-audit.md` and `.context-prime.md` now cover all 4 schema principles (1 existing + 3 new).
- **Fixed missing `SCHEMA-SELF-DESCRIBING` in `catalog.yaml`** — existing principle was present as a file but had no catalog entry; added to new `SCHEMA` section.
- **4 new pipeline principles** in `pipeline` namespace — `PIPELINE-REPRODUCIBLE-BUILDS` (layer 1, with inspection), `PIPELINE-ENVIRONMENT-ISOLATION` (layer 1, with inspection), `PIPELINE-FAIL-FAST-PIPELINE` (layer 1, with inspection), `PIPELINE-DEPLOYMENT-GATES` (layer 2, with inspection). Pipeline namespace expanded from 2 to 6 principles. Sources: Humble & Farley *Continuous Delivery* (ISBN 978-0-321-60191-9), OpenSSF SLSA v1.0, Reproducible Builds Project, OWASP CI/CD Security Cheat Sheet, Forsgren et al. *Accelerate* (ISBN 978-1-942788-33-1).
- **Updated pipeline layer files** — `layers/pipeline/layer-1-universal.md` adds 3 new layer-1 principles; `layers/pipeline/layer-2-contexts.yaml` adds `PIPELINE-DEPLOYMENT-GATES` to deploy context.
- **New `.context-inspect.md` for pipeline** — machine-executable pre-scan patterns for all 6 pipeline principles.
- **Updated pipeline context files** — `.context-audit.md` and `.context-prime.md` now cover all 6 pipeline principles.
- **`REJECTED.md`** — new file documenting considered-but-rejected principles with rationale; prevents re-evaluation of the same candidates.
- **6 new configuration principles** in `config` namespace — `CONFIG-SCHEMA-FIRST`, `CONFIG-EXPLICIT-OVER-CONVENTIONAL`, `CONFIG-ENVIRONMENT-PARITY`, `CONFIG-EXPLICIT-DEFAULTS`, `CONFIG-CHANGE-TRACEABILITY` (layer 2, with contexts), `CONFIG-MINIMAL-SURFACE` (layer 2, with inspection). Sources: JSON Schema specification, Pydantic Settings docs, Spring Boot Reference, 12factor.net Factors III and VII, Humble & Farley *Continuous Delivery*, Beyer et al. *Site Reliability Engineering*, Weaveworks GitOps, OWASP A05:2021, Nygard *Release It!*, Saltzer & Schroeder (Economy of Mechanism), Hunt & Thomas *The Pragmatic Programmer*.
- **Updated `config` context files** — `.context-audit.md` and `.context-prime.md` now cover all 8 config principles (2 existing + 6 new).
- **Updated `layers/config/layer-1-universal.md`** — 4 new layer-1 principles added (`CONFIG-SCHEMA-FIRST`, `CONFIG-EXPLICIT-OVER-CONVENTIONAL`, `CONFIG-ENVIRONMENT-PARITY`, `CONFIG-EXPLICIT-DEFAULTS`).
- **Updated `layers/config/layer-2-contexts.yaml`** — 3 new context triggers (`secrets-management` extended, `version-controlled-config`, `large-config`) activating `CONFIG-CHANGE-TRACEABILITY` and `CONFIG-MINIMAL-SURFACE`.
- **Updated `groups/config.yaml`** — all 6 new principles added to the `@config` group (9 config-specific principles total).
- **8 new documentation principles** in `docs` namespace — `DOC-AS-CODE`, `DOC-CLOSE-TO-CODE`, `DOC-UNIQUE`, `DOC-TASK-ORIENTED`, `DOC-SCANNABLE`, `DOC-OBJECTIVE`, `DOC-SELF-CONTAINED`, `DOC-ADDRESSABLE`. Sources: Gentle *Docs Like Code* (ISBN 978-1365418730), Write the Docs docs-as-code and docs-principles guides, Martraire *Living Documentation* (ISBN 978-0134689326), Procida "Twelve principles of documentation" (vurt.org), Morkes & Nielsen "Concise, SCANNABLE, and Objective" (NN/G, 1997), Carey et al. *Developing Quality Technical Information* 3rd ed. (ISBN 978-0133118971), Baker *Every Page is Page One* (ISBN 978-1937434281), Microsoft Writing Style Guide.
- **Updated `docs` context files** — `.context-audit.md` and `.context-prime.md` extended with all 7 new principles.
- **Updated `groups/docs.yaml`** — all 7 new principles added (13 doc-specific principles total).
- **8 new API design principles** in `code/api` namespace — `CODE-API-RATE-LIMITING` (with inspection), `CODE-API-PROBLEM-DETAILS`, `CODE-API-PAGINATION` (with inspection), `CODE-API-HTTP-CACHING` (with inspection), `CODE-API-CONDITIONAL-REQUESTS` (with inspection), `CODE-API-CONTENT-NEGOTIATION` (with inspection), `CODE-API-API-VERSIONING` (with inspection), `CODE-API-GRPC-PROTOBUF` (with inspection). Sources: RFC 6585, RFC 7807/9457, RFC 5988, RFC 9111, RFC 7232, RFC 7231/9110, RFC 8594, Richardson & Ruby *RESTful Web Services*, Indrasiri & Kuruppu *gRPC: Up and Running*, Google API Design Guide.
- **Context files for `code/api`** — `.context-audit.md`, `.context-prime.md`, and `.context-inspect.md` created, covering all 13 API principles (5 existing + 8 new).

---

## [v0.3.2] — 2026-03-22

### Changed

- **`/audit` explicit principle override** — `/audit` now accepts an explicit principle spec to force a specific principle set, bypassing `.principles` files and dynamic detection entirely. Three equivalent syntaxes are supported:
  - `<spec> on <target>` — natural language: `/audit DDD on src/orders`
  - `<target> --with <spec>` — flag syntax: `/audit src/orders --with DDD`
  - `@<group> <target>` — group-prefix syntax: `/audit @ddd src/orders`
  - Multiple groups supported comma-separated: `/audit clean-arch, solid on src/`
  - `principle_source` in `audit-output.json` reports `explicit: <spec>` when override is active.

---

## [v0.3.1] — 2026-03-19

### Added

- **Version metadata in command frontmatter** — `/audit`, `/prime`, and `/scout` source files now carry `version`, `description`, `argument-hint`, and `authors` fields in YAML frontmatter, stamped at install time from `VERSION`.

### Fixed

- **Copilot CLI global skills management** — `install.sh` and `uninstall.sh` now correctly create, update, and remove `~/.copilot/skills/<name>/SKILL.md` entries for global Copilot CLI installations.

---

## [v0.3.0] — 2026-03-18

### Changed

- **Artifact-type layer system** — `layers/artifact-types.yaml` classifies every reviewed file into one of 6 stacks (`code`, `docs`, `config`, `infra`, `pipeline`, `schema`), each with its own `layer-1-universal.md` and `layer-2-contexts.yaml` (plus `layer-3-risk-signals.yaml` for `code` and `infra`). A shared universal set of 6 principles (`SIMPLE-DESIGN-REVEALS-INTENTION`, `CODE-CS-DRY`, `CODE-CS-KISS`, `CODE-CS-YAGNI`, `CODE-DX-NAMING`, `ARCH-DECISION-RECORDS`) applies across all stacks; stack-specific layers add targeted principles on top. Type detection uses file extension, filename, and path-pattern signals, with `infra` evaluated before `config` to resolve ambiguous YAML files (e.g. `Chart.yaml`, `values.yaml`).

### Added

- **11 new continuous delivery principles** in new `cd` namespace — `CD-TRUNK-BASED-DEVELOPMENT`, `CD-KEEP-BUILD-GREEN` (with inspection), `CD-DEPLOY-ON-EVERY-COMMIT`, `CD-FEATURE-FLAGS` (with inspection), `CD-FAST-FEEDBACK-LOOPS`, `CD-GITOPS`, `CD-BLUE-GREEN-DEPLOYMENT`, `CD-CANARY-RELEASE`, `CD-DEPLOYMENT-SMOKE-TESTS`, `CD-PIPELINE-AS-CODE` (with inspection), `CD-BUILD-ONCE-DEPLOY-MANY` (with inspection). New `groups/cd.yaml`, catalog, and context files created.
- **24 new architecture and integration principles** — 15 in `arch` namespace (Hexagonal Architecture, Saga, Strangler Fig, Layered Architecture, Microkernel, Anti-Corruption Layer, BFF, Bulkhead, Service Layer, Unit of Work, MVC, API Gateway, Data Mapper, Active Record, Transaction Script); 4 DDD strategic patterns in `ddd` namespace (Context Map, Shared Kernel, Open Host Service, Published Language); 5 Enterprise Integration Patterns in new `eip` namespace (Correlation Identifier, Content-Based Router, Dead Letter Channel, Message Filter, Claim Check). `eip` catalog, context, and group files created. `groups/microservices.yaml` and `groups/ddd.yaml` updated.
- **7 new observability principles** in `code/ob` — USE Method (Gregg), RED Method (Wilkie), Error Budget burn-rate alerting (with inspection), Four Golden Signals, Health Check API — Richardson (with inspection), Percentile-based latency (Dean & Barroso), Alert on symptoms not causes. `groups/microservices.yaml`, context files, and `catalog.yaml` (242 principles) updated.
- **7 new testing principles** in `code/ts` — Test Data Builder, Humble Object, No Test Logic in Production (with inspection), Characterization Tests (`Audit-scope: limited`), Test Pyramid, Consumer-Driven Contracts, Property-Based Testing.
- **Audit-scope metadata** — `principles/AUDIT-SCOPE.md` added; 8 principle files annotated (4 excluded, 4 limited).
- **`CONTRIBUTING.md`** — code auditability and no-redundancy requirements added.
- **`principles/TEMPLATE.md`** — optional `**Audit-scope:**` field documented.

---

## [v0.2.0] — 2026-03-17

### Changed

- **Installer copies principle data to `~/.principles`** — created on install, refreshed on every run; `{{PRINCIPLES_DIRECTORY}}` placeholder substituted at install time in command files. Global uninstall removes `~/.principles`; local uninstalls leave it intact.

### Added

- **14 new database principles** in new `db` namespace — `DB-ACID`, `DB-SCHEMA-MIGRATIONS-AS-CODE`, `DB-CAP-THEOREM`, `DB-AVOID-N-PLUS-ONE` (with inspection), `DB-INDEX-FOR-ACCESS-PATTERNS`, `DB-THIRD-NORMAL-FORM`, `DB-CQRS`, `DB-OUTBOX-PATTERN`, `DB-EVENTUAL-CONSISTENCY`, `DB-EVENT-SOURCING`, `DB-OPTIMISTIC-CONCURRENCY`, `DB-TWO-PHASE-LOCKING`, `DB-POLYGLOT-PERSISTENCE`, `DB-DENORMALIZE-INTENTIONALLY`. New `@db` group and context files.
- **7 new security principles** — 4 in `code/sec` (`DEFENSE-IN-DEPTH`, `FAIL-SAFE-DEFAULTS` with inspection, `COMPLETE-MEDIATION`, `PRIVACY-BY-DESIGN`) and 3 in new `sec-arch` namespace (`THREAT-MODELLING`, `ZERO-TRUST`, `SUPPLY-CHAIN-SECURITY` with inspection). `groups/security-focused.yaml` updated.
- **27 new OOP/object-design principles** — `pkg` namespace (6 Package Principles, Martin); `gof` additions (Law of Demeter, Null Object); `code/cs` additions (Design by Contract, Tell Don't Ask, Information Hiding, Uniform Access); 9 Fowler code smells; 5 Effective Java items; `DDD-SPECIFICATION`.
- **20 functional programming principles** in new `fp` namespace — 4 universal (pure functions, referential transparency, immutability, no shared mutable state), 16 contextual. New `@fp` group and 11 new language groups (`@javascript`, `@swift`, `@ruby`, `@php`, `@scala`, `@cpp`, `@c`, `@dart`, `@elixir`, `@haskell`, `@fsharp`).

---

## [v0.1.0] — 2026-03-15

**Initial release.**

### Highlights

- **187 principle files** across **13 top-level namespaces** — `12factor`, `arch`, `clean-arch`, `code`, `code-smells`, `ddd`, `effective-java`, `gof`, `grasp`, `infra`, `owasp`, `simple-design`, `solid`
- **30 pre-defined groups** — `@spring-boot`, `@react`, `@angular`, `@django`, `@fastapi`, `@microservices`, `@security-focused`, `@clean-arch`, `@solid`, `@typescript`, and more
- **3 AI commands** — `/scout`, `/prime`, `/audit`
- **3-layer model** — Universal, Contextual, and Risk-Elevated principles
- **Hierarchical `.principles` file resolution** — project-level overrides with inheritance
- **Cross-platform installer** — Bash, PowerShell, and CMD wrapper scripts
- **3 target platforms** — Claude Code, GitHub Copilot, Cursor
- **Full documentation suite** — README, DESIGN.md, INSTALL.md, REQUIREMENTS.md, and more
- **Inspection sections** — `.context-inspect.md` files and inline `## Inspection` sections with `grep` patterns for automated principle verification across `code/` and `solid/` namespaces
- **Improved catalog** — restructured `principles/catalog.yaml` with expanded metadata
- **Enhanced audit command** — richer inspection-driven audit flow in `targets/claude-code/audit.md`
- **CONTRIBUTING.md** — contributor guidelines added
- **Layer refinements** — updated universal layer, context mappings, and risk signals

### What's Next

See [TODO.md](TODO.md) for the roadmap.

---

[v0.3.2]: https://github.com/dot-principles/dot-principles/releases/tag/v0.3.2
[v0.3.1]: https://github.com/dot-principles/dot-principles/releases/tag/v0.3.1
[v0.3.0]: https://github.com/dot-principles/principles/releases/tag/v0.3.0
[v0.2.0]: https://github.com/dot-principles/principles/releases/tag/v0.2.0
[v0.1.0]: https://github.com/dot-principles/principles/releases/tag/v0.1.0
