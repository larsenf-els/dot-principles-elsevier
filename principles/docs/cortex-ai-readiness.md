# DOC-CORTEX-AI-READINESS — Documentation is structured for reliable AI consumption

**Layer:** 2 (contextual)
**Categories:** documentation, ai-readiness, accessibility
**Applies-to:** docs

## Principle

Documentation intended for use by AI agents — whether for code generation, question answering, or automated review — must be consistently structured so that AI models can parse, reference, and reason about it without ambiguity. This means well-formed Markdown, consistent heading hierarchies, language-tagged code blocks, and an `AGENTS.md` file that declares the project context and permitted AI actions.

AI models interpret structure as semantics. A skipped heading level, a bare URL, or an unlabelled code block each introduce noise that degrades the quality of AI-generated output derived from the documentation.

## Why it matters

AI systems rely on structural cues to segment and interpret documentation. When those cues are missing or inconsistent, the model may misattribute code samples, lose section context, or misread table data. As AI-assisted development matures, the quality of documentation as a machine-readable artifact becomes as important as its readability for humans.

## Violations to detect

- **P8 (MUST)** — `AGENTS.md` is absent or does not contain the required sections: project description, permitted actions, prohibited actions
- **P1 (SHOULD)** — A Markdown file skips heading levels (e.g., jumps from `##` to `####` without an intervening `###`)
- **P2 (SHOULD)** — A fenced code block does not declare a language specifier (e.g., ` ``` ` instead of ` ```python `)
- **P3 (SHOULD)** — A Markdown file contains markup artifacts: stray HTML tags, escaped Markdown syntax that renders as literal characters, or broken entity references
- **P4 (SHOULD)** — A Markdown table is present but lacks a header row and separator line
- **P5 (SHOULD)** — A bare URL is used instead of Markdown link syntax (`[label](url)`)
- **P6 (SHOULD)** — An image element does not provide a descriptive `alt` attribute (empty alt or generic text such as "image" or "screenshot")
- **P7 (SHOULD)** — A document makes references to related documents without using Markdown cross-reference links

## Good practice

- Add an `AGENTS.md` at the repository root describing: what the project does, what AI agents are permitted to do (generate tests, refactor, update docs), and what is prohibited (modifying release scripts, credentials, generated files)
- Always specify a language on fenced code blocks — use `text` or `console` for shell sessions without a language
- Run a Markdown linter (e.g., `markdownlint`) in CI to catch heading hierarchy violations and bare URLs automatically
- Use `[label](relative-path.md)` for cross-references between documentation pages rather than reproducing content inline
- Write descriptive alt text that conveys the meaning of an image, not just its file name

## Sources

- GitHub. "Creating an AGENTS.md file." GitHub Copilot documentation. https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot (accessed 2026-03-20).
- Gruber, John. "Markdown: Syntax." https://daringfireball.net/projects/markdown/syntax (accessed 2026-03-20).
- Elsevier Engineering. "Cortex Documentation Standards." Internal engineering handbook, 2025.
