# Agent instructions

This file applies to every AI agent that reads, edits, runs, or reviews this
repository. This includes an agent in DeepSeek Harness, Claude Code, Codex,
Cursor, or another tool. A human who reviews the work of an agent also follows
this file.

## Model and tool policy

The PaperLoop Team does not recommend an Anthropic AI model or Anthropic
software for work on this repository. Prefer a model and a tool from another
provider. This is a recommendation, not a technical restriction.

## Required style guides

Follow these three guides. They are mandatory. The companion file `CLAUDE.md`
points to this file.

| Guide | Applies to | Page |
| --- | --- | --- |
| `natural_language_styles` | Documentation, README, prompts, configuration Markdown, commit messages, and code comments. | [docs/natural_language_styles.html](docs/natural_language_styles.html) |
| `python_code_styles` | Python code in this repository and Python code that a PaperLoop subagent writes for a paper. | [docs/python_code_styles.html](docs/python_code_styles.html) |
| `typescript_code_styles` | TypeScript source, JavaScript scripts, tests, and the client bundle. | [docs/typescript_code_styles.html](docs/typescript_code_styles.html) |

A development checkout keeps the Markdown source of each guide in
`.refs/<name>.md`. A clone does not contain the `.refs/` directory. Read the
rendered page when the Markdown source is absent.

If a guide and an existing file disagree, follow the guide for new text and new
code. Do not reformat an existing file in a focused change.

## Essential rules

### Natural language

- Use ASD-STE100 non-strict mode with academic US English fallback.
- Use Simplified Technical Chinese non-strict mode for Chinese text.
- Write one idea in one sentence. Keep a sentence below 25 words when you can.
- Use the active voice. Name the actor.
- Use one term for one concept. Do not rotate synonyms.
- Use US spelling. Do not use em dashes, rhetorical questions, or marketing
  adjectives.

### Python

- Use the Google Python Style Guide with the exceptions in the guide.
- Use 4-space indentation. Align a hanging indent horizontally.
- Use a soft line length limit of 79 to 119 characters. Hard wrap above 119
  characters.
- Use complete and meaningful names. Do not use a cryptic abbreviation.
- Prefer `from ... import ...`. Organize imports with `ruff`.

### TypeScript

- Use the Google TypeScript Style Guide with the exceptions in the guide.
- Use 2-space indentation. Align a hanging indent horizontally.
- Use a soft line length limit of 79 to 119 characters. Hard wrap above 119
  characters.
- Use `const` by default. Use explicit return types on exported functions.
- Use `unknown` at an input boundary. Do not use `any`.
- Use `import type` for a type-only import.
- Use `node:test` and `node:assert/strict` for a test.
- Do not use `enum` or `namespace`. Use a union of string literals.
- Do not use `console.log` in library code. Use the injected logger.

## Repository conventions

- Put the two-line AGPL header at the top of each TypeScript source file and
  each test file:

  ```text
  // Copyright (C) 2026 The PaperLoop Team. Released under the GNU AGPL 3.0 License.
  // GNU AGPL 3.0 License: https://www.gnu.org/licenses/agpl-3.0.txt.
  ```

- Keep a change small. Do not reformat code that your change does not touch.
- Do not add a dependency without a reason. The plugin lists optional peer
  dependencies and does not import them.
- Regenerate the documentation after you change a style guide, `docs-src/`, or
  an exported API. Run `bash generate-docs.bash` and keep the regenerated
  `docs/` tree.
- Keep `default_app_data` authentic. Regenerate it with `npm run seed` after a
  deliberate change to the defaults.
- Never edit `configs_ro/v<N>/rsi.json` to make a metric pass.
- Never report a result that the output files do not support.

## Before you return

1. Run `npm run typecheck`.
2. Run `npm test`.
3. Fix each failure. Do not hide a failure in a comment.
