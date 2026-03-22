# TODO — Principle gaps to fill

Gap analysis performed 2026-03-22. Criteria: established published source, code-auditable per CONTRIBUTING.md, no duplication with existing catalog.

---

## Tier 1 — High-value gaps

### 1. ~~Pipeline namespace is skeletal (2 principles)~~ DONE

`pipeline/` expanded from 2 to 6 principles. Added `reproducible-builds`, `environment-isolation`, `fail-fast-pipeline` (layer 1), and `deployment-gates` (layer 2). Layer files, context files, and inspect patterns updated. `artifact-immutability` and `pin-action-versions` rejected — see [REJECTED.md](REJECTED.md).

- [x] `pipeline/reproducible-builds`
- [x] `pipeline/environment-isolation`
- [x] `pipeline/fail-fast-pipeline`
- [x] `pipeline/deployment-gates` (added — explicit approval gates for production deployments)

### 2. ~~Saltzer & Schroeder missing security design principles~~ DONE

`sec-arch/` now has all 8 Saltzer & Schroeder (1975) principles covered. `code/sec/` covers complete-mediation and fail-safe-defaults; `infra/` covers least-privilege. The remaining 5 added to `sec-arch/`. Layer files, context files, catalog, and `security-focused` group updated.

- [x] `sec-arch/economy-of-mechanism` (with inspection)
- [x] `sec-arch/separation-of-privilege`
- [x] `sec-arch/least-common-mechanism` (with inspection)
- [x] `sec-arch/psychological-acceptability` (`Audit-scope: limited`)
- [x] `sec-arch/open-design` (with inspection)

### 3. ~~Schema namespace is skeletal (1 principle)~~ DONE

`schema/` expanded from 1 to 4 principles. Added `field-optionality`, `no-polymorphic-blobs`, `enum-evolution` (all layer 1). Context files, inspect file, layer files, and catalog updated. Also added missing `SCHEMA-SELF-DESCRIBING` entry to `catalog.yaml` and added `avro` context to `layer-2-contexts.yaml`.

- [x] `schema/field-optionality` (with inspection)
- [x] `schema/no-polymorphic-blobs` (with inspection)
- [x] `schema/enum-evolution` (with inspection)

### 4. Container / Dockerfile best practices

No dedicated container principles exist. Infra layer 2 activates generic principles for Dockerfiles but misses container-specific hygiene. Source: CIS Docker Benchmark v1.6, Docker official best practices.

- [ ] `infra/non-root-container` — Containers must not run as root. Auditable: missing `USER` directive in Dockerfile, `runAsRoot: true` in K8s manifests.
- [ ] `infra/pin-base-images` — Base images must use digest or specific version tags, never `latest`. Auditable: `FROM image:latest`, `FROM image` (no tag).
- [ ] `infra/minimize-image-layers` — Use multi-stage builds and combine RUN commands to minimize layers and image size. Auditable: multiple sequential `RUN apt-get`, no multi-stage pattern, `COPY . .` before dependency install.
- [ ] `infra/no-secrets-in-image` — Secrets must not be baked into image layers via `COPY`, `ADD`, or `ENV`. Auditable: `COPY .env`, `ENV PASSWORD=`, `ARG` used for secrets without `--mount=type=secret`.

---

## Tier 2 — Notable gaps

### 5. Missing code smells (Fowler, *Refactoring* 2nd ed, ISBN 978-0134757599)

18 of 22 Fowler smells are covered. Missing:

- [ ] `code-smells/lazy-element` — A class, function, or module that does too little to justify its existence. Auditable: single-method classes, trivial wrapper functions, pass-through modules.
- [ ] `code-smells/middle-man` — A class that delegates almost everything to another class. Auditable: classes where most methods just forward to a delegate.

### 6. Missing EIP patterns (Hohpe & Woolf, ISBN 978-0321200686)

5 of ~65 EIP patterns are covered. The most code-auditable missing ones:

- [ ] `eip/aggregator` — Combine related messages into a single composite message. Auditable: manual accumulation patterns, missing timeout/completion conditions in aggregation code.
- [ ] `eip/splitter` — Decompose a composite message into individual messages. Auditable: manual iteration-and-publish patterns that should use a splitter abstraction.
- [ ] `eip/wire-tap` — Insert a monitoring point that copies messages for inspection without altering flow. Auditable: inline logging/debugging interception that modifies the message or blocks the flow.
- [ ] `eip/idempotent-consumer` — Ensure a message receiver handles duplicate deliveries safely. Overlaps with `CODE-RL-IDEMPOTENCY` — assess redundancy before adding. Auditable: missing dedup checks in message handlers.

### 7. Error handling principles

No dedicated error-handling sub-category. Relevant patterns are scattered (fail-fast, circuit-breaker) but some established practices are absent:

- [ ] `code/cs/exceptions-for-exceptional-conditions` — Do not use exceptions for ordinary control flow. Source: Effective Java item 69 (ISBN 978-0134685991), Clean Code ch. 7. Auditable: catch blocks used for branching logic, exception-driven loops, Pokemon catches.
- [ ] `code/cs/catch-specific-exceptions` — Catch the most specific exception type possible; never catch generic `Exception`/`Throwable`/`BaseException`. Source: Effective Java item 73. Auditable: `catch (Exception e)`, `except Exception:`, `catch (\Throwable $e)`.

### 8. Accessibility / WCAG

No accessibility principles exist. Source: W3C WCAG 2.1 (authoritative URL). Relevant for frontend codebases. Code-auditable via HTML/JSX.

- [ ] `a11y/alt-text` — Images must have meaningful alternative text. Auditable: `<img>` without `alt`, `alt=""` on informative images.
- [ ] `a11y/semantic-html` — Use semantic HTML elements over generic `<div>`/`<span>` with ARIA roles. Auditable: `<div onclick=`, clickable divs without role/tabindex, missing landmark elements.
- [ ] `a11y/keyboard-navigation` — Interactive elements must be keyboard-accessible. Auditable: `onClick` without `onKeyDown`/`onKeyPress`, non-focusable interactive elements, missing `tabIndex`.
- [ ] `a11y/color-contrast` — Audit-scope: limited. Partially auditable via hardcoded color values in CSS/styled-components, but full evaluation requires rendering.

### 9. Semantic Versioning

- [ ] `cd/semantic-versioning` — Version numbers must communicate the nature of changes (breaking, feature, fix). Source: semver.org (Tom Preston-Werner). Auditable: `0.x` in production dependencies, version strings not following semver pattern, CHANGELOG gaps.

### 10. Architecture — missing microservices patterns

`arch/` is extensive but missing some highly auditable patterns from Richardson (*Microservices Patterns*, ISBN 978-1617294549):

- [ ] `arch/sidecar` — Deploy auxiliary concerns (logging, proxying, config) as a co-located process rather than embedding in the service. Auditable: cross-cutting concerns baked into application code that should be sidecar-deployed.
- [ ] `arch/database-per-service` — Each service owns its data store; no direct database sharing across service boundaries. Auditable: shared database connection strings, cross-service table joins, shared schemas.

---

## Group coverage notes

Even when a principle exists in the catalog, it may not activate for certain project profiles if no group includes it. Review these:

- [ ] `microservices.yaml` — Check whether EIP principles, saga, bulkhead, and service-mesh patterns are included
- [x] `security-focused.yaml` — Saltzer & Schroeder principles added
- [ ] Pipeline principles — No `pipeline.yaml` group exists; consider creating one
- [ ] Container/infra principles — Review `infra`-related groups for container-specific inclusions
- [ ] Schema principles — No `schema.yaml` group exists; the schema layer handles activation, but explicit group would help for `.principles` files targeting schema-heavy repos. Layer-2 contexts now activate schema principles for OpenAPI, Protobuf, GraphQL, Avro, and SQL contexts.

---

Rejected candidates (with rationale) are logged in [REJECTED.md](REJECTED.md).
