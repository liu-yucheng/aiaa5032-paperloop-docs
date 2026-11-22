# aiaa5032-paperloop

A DeepSeek Harness plugin for autonomous paper reproduction, critical analysis, and self-evolution.

## Introduction

PaperLoop takes one paper PDF and a public code repository.
It reproduces the computational result of that paper and writes two critical reports.
A forward pass runs six stages through five isolated subagents: runtime setup, reproduction code,
reproduction report, innovation code, innovation report, and self-evaluation.
A backward pass runs stage 7, self-evolution, and writes the next configuration revision.
The plugin allows 1080 seconds for a forward, validation, or test pass, and 180 seconds for a
backward pass.
Each stage has one soft time limit and one hard time limit of twice the soft limit.
All subagents keep temporary files in dot-basename directories and delete them before a stage returns.
The Coder subagent writes Python, C, C++, R, MATLAB, Fortran, TypeScript, JavaScript, or SQL.
It refactors the reusable parts into a library under `code/source/` and generates a documentation
website under `code/docs/`.
The plugin scores the run with TCR, HIB, DCC, and token cost efficiency, then proposes a new configuration for the next session.
This repository is an implementation of AIAA5032 (taught at HKUST (GZ) in the Fall 2026-2027 semester)
course project PaperLoop.
View the documentation [at this link](https://github.com/liu-yucheng/aiaa5032-paperloop-docs).

## Versions

This repository holds the documentation of the plugin repository
`aiaa5032-paperloop`. The documentation has no version of its own. Every
version tag here must have a plugin version tag with the same name. For
example, tag `v0.12.0` here holds the documentation of plugin tag `v0.12.0`.

A plugin release that changes no documentation gets no documentation tag. A
documentation correction that no plugin tag supports stays untagged until the
next plugin tag.

## AI agents

AI agents develop and maintain this repository. [`AGENTS.md`](./AGENTS.md) holds
the binding instructions for every agent that touches this repository.
Each agent must follow these style guides:

- [`natural_language_styles`](./docs/natural_language_styles.html)
- [`python_code_styles`](./docs/python_code_styles.html)
- [`typescript_code_styles`](./docs/typescript_code_styles.html)

The team does not recommend Anthropic AI models or software for work on this
repository. This is a recommendation, not a technical restriction.

## Usage

The plugin adds ten tools and eight commands to DeepSeek Harness.

### Requirements

- DeepSeek Harness 0.2.0 or later.
- Node.js 22.19 or later, or Node.js 24 or later.
- `uv` for Python environments and dependencies.
- The native toolchain that the reproduced paper needs: a C, C++, or Fortran compiler, or
  an R, MATLAB, or Node.js runtime.
- At least one documentation generator: `pdoc` or MkDocs for Python, Doxygen for C, C++,
  MATLAB, and Fortran, `pkgdown` for R, TypeDoc or JSDoc for TypeScript and JavaScript, and
  SchemaSpy or `tbls` for SQL.
- Python with matplotlib for the report figures and the report animations.
- Git when the paper links a code repository.

The plugin lists optional peer dependencies.
It does not import them.
Install only the plugins that you use.

### Installation

Build the package first:

```bash
npm install
npm run build
```

Then add the absolute package directory as a bundle in the DeepSeek Harness profile. The patch adds this row:

```yaml
- insert:
    - id: aiaa5032-paperloop
      name: dsh-aiaa5032-paperloop
```

Do not edit the profile by hand, because the plugin manager validates the package and the bundle patch.

After the bundle is enabled, run `/paperloop_forward <pdf> [...]` to start one paper pass, and
run `/paperloop_backward` to apply the pending evolution plans.

The main command is `/paperloop` with the `forward`, `validate`, `test`, `feedback`,
`backward`, `help`, or `clear` action.
The shortcuts are `/paperloop_forward`, `/paperloop_validate`, `/paperloop_test`,
`/paperloop_feedback`, `/paperloop_backward`, `/paperloop_help`, and
`/paperloop_clear_appdata`.

- `/paperloop_forward <pdf> [...]` runs stages 1 to 7. It writes the evaluation record to
  `evals/pending/` and the evolution plan to `evolutions/pending/`.
- `/paperloop_backward [<index|session> ... | --all]` runs stage 8 and writes the next
  `configs_rw/v<N+1>/` revision.
- `/paperloop_validate <pdf> [...]` writes the loss to `evals/validated/` and one decision.
  A rollback needs a loss that grows worse for three consecutive passes by default.
- `/paperloop_test <pdf> [...]` writes the loss to `evals/tested/` and one report.
- `/paperloop_feedback --session=<index|session> --feedback=<text> [...]` adds human feedback
  to one pending session. It re-runs the evaluator and rewrites the plan.
- `/paperloop_help [--topics <topics>]` prints the usage line of every command and the live state.
  With `--topics` a subagent writes one detailed page for those topics.
- `/paperloop_clear_appdata [--yes]` deletes the app data and restores the packaged seed.

The ten tools are the tool form of the eight commands.
The tools `paperloop_status`, `paperloop_audit`, and `paperloop_config` have no command.
Read the generated pages in [`docs/index.html`](./docs/index.html) for the full documentation.

## The PaperLoop Team

The PaperLoop Team develops and maintains this plugin:

- CHEN Fangda
- HUANG Junkai
- LIU Chang
- LIU Yucheng
- RONG Yan

All members contribute equally.
Audit your contribution and treat your teammates equally.

## Copyright

```text
Copyright (C) 2026 The PaperLoop Team. Released under the GNU AGPL 3.0 and CC BY-NC-SA 4.0 Licenses.

Textual contents are released under the GNU AGPL 3.0 License.
See [LICENSE](./LICENSE) and https://www.gnu.org/licenses/agpl-3.0.txt.

Non-textual contents are released under the CC BY-NC-SA 4.0 License.
See [license-2](./license-2) and https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode.txt.
```
