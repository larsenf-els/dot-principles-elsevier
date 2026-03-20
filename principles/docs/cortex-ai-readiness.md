# DOC-CORTEX-AI-READINESS — Documentation is structured for reliable AI consumption

**Layer:** 2 (contextual)
**Categories:** documentation, ai-readiness, accessibility
**Applies-to:** docs

## Principle

Documentation intended for use by AI agents must be consistently structured so that models can parse, reference, and reason about it without ambiguity. This means well-formed Markdown (consistent heading hierarchy, language-tagged code blocks, clean tables, named links, descriptive alt text, internal cross-references) and an `AGENTS.md` file declaring the project context and permitted AI actions.

AI models interpret structure as semantics. A skipped heading level, an unlabelled code block, or a bare URL each introduce noise that degrades the quality of AI-generated output.

This principle maps directly to the **AI Readiness Checker** from [agent-ready-docs](https://github.com/elsevier-centraltechnology/agent-ready-docs). Run it with:

```bash
node ./bin/agent-ready-docs.js check --checker ai-readiness --repo-path /path/to/your/repo
```

Checks P1–P7 are scored per file across all in-scope Markdown files (`docs/**/*.md`, `README.md`, `CONTRIBUTING.md`, `AGENTS.md`, `*.md`). P8 is a single repository-level signal scored separately.

See the [reference](https://github.com/elsevier-centraltechnology/agent-ready-docs/blob/main/docs/reference/ai-readiness-checker.md) and [explanation](https://github.com/elsevier-centraltechnology/agent-ready-docs/blob/main/docs/explanation/ai-readiness-checks.md) docs for full details.

## Why it matters

AI systems rely on structural cues to segment and interpret documentation. When those cues are missing or inconsistent, the model may misattribute code samples, lose section context, or misread table data. A file can exist and contain all the right sections and still be structurally fragile for AI consumption. Without `AGENTS.md`, AI coding agents invent their own operating rules and may propose changes to protected files or skip required reviews with high confidence.

## Violations to detect

These are the exact checks run by the AI readiness checker.

**Per-file checks (P1–P7)**

- **P1** — A Markdown file has no H1 heading, or skips heading levels (e.g., H1 → H3 without an intervening H2; detected by comparing consecutive heading levels: `headings[i].level > headings[i-1].level + 1`)
- **P2** — A fenced code block (` ``` `) has no language specifier on its opening fence; or two or more consecutive lines outside fenced blocks are indented 4+ spaces and contain code-like characters (`{}();:=><[]$\``)
- **P3** — Outside of fenced code blocks, the file contains: inline HTML tags (`<tag>`), Confluence macros (`{panel}`, `{color}`, `{toc}`, `{noformat}`, `{code}`), or wiki-style double-bracket markup (`[[...]]`)
- **P4** — A Markdown table row is followed by another table row without an intervening separator line (pattern: `| :---: |`); i.e., a table exists but the header separator is missing
- **P5** — A bare `http://` or `https://` URL appears in prose (outside fenced code blocks and outside a Markdown link label or parenthesis)
- **P6** — An image (`![...](...)`) has empty alt text, or generic alt text (`image`, `img`, `screenshot`, `diagram`); or a section whose heading matches `quick start|instruction|steps?|how to|example` contains an image but no prose, code, or list content alongside it
- **P7** — The file contains no named Markdown links (`[label](target)`) to internal documents (targets that do not start with `http`, `https`, `mailto`, or `#`)

**Repository signal (P8)**

- **P8** — `AGENTS.md` is absent at the repository root; or is empty; or does not contain all three of: a project description (`project description`, `about`, or `overview`), permitted actions (`permitted`, `expected actions`, or `allowed`), and prohibited actions (`prohibited`, `constraints`, `not allowed`, or `forbidden`)

## Good practice

- Always specify a language on fenced code blocks — use `text` or `console` for shell output without a specific language
- Run `markdownlint` in CI to catch heading hierarchy violations and bare URL patterns automatically
- Use `[label](relative-path.md)` for cross-references between documentation pages rather than reproducing content inline
- Write descriptive alt text that conveys the meaning of an image, not just its filename; if a diagram is the only place a concept is explained, reproduce that explanation in prose alongside it
- Add `AGENTS.md` at the repository root with at minimum: what the project does (project description), what AI agents may do (permitted actions), and what they must not do (prohibited actions)

## Sources

- Stack, Joyce. "AI Readiness Checker." *agent-ready-docs* reference documentation. https://github.com/elsevier-centraltechnology/agent-ready-docs/blob/main/docs/reference/ai-readiness-checker.md (accessed 2026-03-20).
- Stack, Joyce. "AI Readiness Checks." *agent-ready-docs* explanation documentation. https://github.com/elsevier-centraltechnology/agent-ready-docs/blob/main/docs/explanation/ai-readiness-checks.md (accessed 2026-03-20).
- Gruber, John. "Markdown: Syntax." https://daringfireball.net/projects/markdown/syntax (accessed 2026-03-20).
