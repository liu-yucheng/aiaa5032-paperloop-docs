# aiaa5032-paperloop

A DeepSeek Harness plugin for autonomous paper reproduction, critical analysis, and self-evolution.

## Introduction

PaperLoop reproduces the computational result of one paper and writes two critical reports.
It runs seven stages in order through five isolated subagents: runtime setup, reproduction code, reproduction report,
innovation code, innovation report, self-evaluation, and self-evolution.
Each stage has one explicit time limit.
All subagents keep temporary files in dot-basename directories and delete them before a stage returns.
The plugin scores the run with TCR, HIB, DCC, and token cost efficiency, then proposes a new configuration for the next session.
This repository is an implementation of AIAA5032 (taught at HKUST (GZ) in the Fall 2026-2027 semester)
course project PaperLoop.
View the documentations [at this link](https://github.com/liu-yucheng/aiaa5032-paperloop-docs).

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

The plugin adds five tools and the `/paperloop` command to DeepSeek Harness.

### Requirements

- DeepSeek Harness 0.2.0 or later.
- Node.js 22.19 or later, or Node.js 24 or later.
- `uv` for Python environments and dependencies.
- Typst, or `uvx --from typst typst` as a fallback. The researcher must compile `report.typ` to `report.pdf`.
- Git for the original code repository.

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

After the bundle is enabled, call `paperloop_setup` with the paper and the repository, then call `paperloop_run`.
A dry run shows the planned stages without starting a subagent.

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
