# Ledger

The public website for QuantSingularity.

[![Live Site](https://img.shields.io/badge/Website-Live-E8A33D?style=for-the-badge)](https://quantsingularity.github.io/Ledger/)&nbsp;&nbsp;
[![GitHub Org](https://img.shields.io/badge/GitHub-QuantSingularity-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/quantsingularity)

Ledger is a searchable, self-contained index of every repository across the organization, styled after a trading blotter rather than a typical landing page: a live ticker tape, a `grep`-style filterable table, and a manifest of the engineering principles the org holds its projects to.

---

## What it is

A single static HTML file. No build step, no framework, no dependencies beyond two Google Fonts. It is meant to be easy to read, easy to fork, and easy to keep in sync with the org's actual repository list.

**Sections:**

| Section                                    | What it does                                                                                                                                           |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Ticker**                                 | A continuously scrolling tape of every repo name and its primary language, paused on hover                                                             |
| **Hero**                                   | Mission statement and live counts (repositories, domains, languages, principles)                                                                       |
| **What We Build / Engineering Principles** | A two-panel manifest, styled as a code comment block and a set of `assert` statements                                                                  |
| **The Index**                              | The core of the site: a `grep`-style search bar, domain filter chips, and a table of every repo with inline match highlighting and a live result count |
| **Contribute**                             | The org's contribution steps and a collaboration contact link                                                                                          |

## Tech stack

| Layer                     | Choice                                                                                                                                                   |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Markup, styling, behavior | Vanilla HTML, CSS, and JavaScript (no build tools, no package manager)                                                                                   |
| Typography                | [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono) and [IBM Plex Sans](https://fonts.google.com/specimen/IBM+Plex+Sans) via Google Fonts |
| Data                      | Repository data is embedded directly in the page as a JavaScript array, no external API or database                                                      |

## Updating the repository index

The table on the site is generated from a single JavaScript array near the bottom of `index.html`:

```js
const REPOS = [
  { name: "...", url: "...", desc: "...", lang: "...", domain: "..." },
  ...
];
```

To add, remove, or correct a project, edit this array directly. `domain` must match one of the six category codes used by the filter chips:

| Code             | Filter chip label   |
| ---------------- | ------------------- |
| `FULLSTACK.APPS` | Fullstack Apps      |
| `INFRA.CORE`     | Platform Infra      |
| `AGENTS.MULTI`   | Multi-Agent AI      |
| `RESEARCH.DL`    | Deep Learning       |
| `LIBS.ENGINES`   | Libraries & Engines |
| `RESEARCH.NB`    | Notebooks           |

No other part of the page needs to change. The ticker, table, counts, and filters all render from this one array.

## Deployment

This repo is deployed via GitHub Pages as a project site. Any push to the default branch that touches `index.html` is picked up automatically once Pages is enabled in **Settings → Pages**.

## Design notes

The palette and type system are defined as CSS custom properties at the top of `index.html`:

| Token     | Value          | Use                                         |
| --------- | -------------- | ------------------------------------------- |
| `--bg`    | `#0A0D12`      | Base background                             |
| `--amber` | `#E8A33D`      | Primary accent                              |
| `--teal`  | `#4FD1AE`      | Secondary accent (C++ tag, positive states) |
| `--rose`  | `#E1667C`      | Tertiary accent (Java tag)                  |
| `--mono`  | JetBrains Mono | Headings, data, code                        |
| `--sans`  | IBM Plex Sans  | Body copy                                   |

Keep new UI within this token set rather than introducing new one-off colors. That is what keeps the site looking like one coherent system rather than a stack of separately designed sections.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
