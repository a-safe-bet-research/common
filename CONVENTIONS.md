# A Safe Bet repository conventions

These rules apply to every repository in the `a-safe-bet-research` organisation. New study repositories are created from `template-study`, which already follows them.

## 1. Where things live

| Where | What |
|---|---|
| OSF Registries | Preregistrations. Registered before data access or analysis; never edited afterwards. |
| Preprint server | The manuscript before publication. Not stored in any repository. |
| GitHub (this organisation) | Working code, documentation and shareable materials, under version control. |
| Zenodo | A fixed, DOI-stamped copy of a repository at each submission and publication. |
| Data repository | Research data, held separately. Never in GitHub. |

The OSF projects created before September 2026 are a frozen historical record. Nothing on them is renamed or removed. New material goes to GitHub.

## 2. Repositories

One repository per study, named for its content in lowercase with hyphens: `framework`, `poc`, `player-perspectives`. No paper numbers, no dates, no author names. Programme-level material goes in `common`.

Repositories start private. A repository becomes public when the associated manuscript is submitted, unless the operator agreements or ethics approval require otherwise. Only organisation owners change visibility.

## 3. Folders

Every study repository has the same top level. Each folder has a one-line test.

| Folder | Test |
|---|---|
| `protocol/` | Was it written before the data existed to say what would be done and why? Preregistration copy, protocol, design documents, study-specific ethics in `protocol/ethics/`. |
| `materials/` | Could another researcher pick it up and use it in their own study? Instruments, guides, coding frames, taxonomies, frameworks. |
| `code/` | Was it run? Analysis scripts and the environment lockfile. |
| `outputs/` | Did it come out of the code? Tables in `outputs/tables/`, figures in `outputs/figures/`. |
| `data/` | The data access statement (`data/README.md`), shareable derived data in `data/derived/`, and an always-empty `data/raw/`. |

Subfolders inside these are free. Where a manuscript cites OSF folders by number, the repository uses the same numbers so appendix references resolve in both places.

No `manuscript/` folder. Programme-level ethics approvals and the DMP live once, in `common/governance/`, and study repositories link to them.

`common` has four folders, each a category: `governance/` (how the programme is allowed to operate), `data-documentation/` (what the data are), `design/` (what was built), `assets/` (what things look like). A folder is created when it has content; the names do not change.

## 4. File names

Lowercase, `snake_case`, no spaces, no brackets. Scripts carry a two-digit run-order prefix (`00_config.R`, `01_build.R`). Dated documents put an ISO date first (`2026-07_analysis_preregistration.pdf`). No version suffixes on code; git is the version. The only permitted suffixes are on documents that record a submitted state: `_submitted`, `_r1`, `_accepted`.

## 5. Code and environments

Analyses are R projects. Each `code/` folder contains an `renv.lock` (or the equivalent for whatever tooling the study uses) so the environment can be restored. Scripts read input paths and credentials from `.Renviron` or a `config.yml` that is never committed. Scripts must run from the repository root in numbered order.

## 6. What never enters a repository

- Participant-level or account-level data in any form, including pseudonymised
- Operator exports, extracts, or files named after an operator
- Credentials, tokens, connection strings, server paths
- Anything covered by a data-sharing agreement that has not passed the data review

The `.gitignore` blocks these by folder, file type and name pattern. It is a safety net, not the rule. Before every commit, check the file list. If in doubt, the file goes in `data/raw/`, which is ignored.

## 7. Data

Each study runs a data review before anything is shared, classifying every dataset as open, derived or aggregated only, controlled access, or not shareable. The result is written in `data/README.md` and summarised in the README's Data availability section. Restricted data go to an approved repository with controlled access; the repository README states how to request it. Derived data in `data/derived/` must be aggregate or synthetic and must not permit re-identification.

## 8. README

Every study README has the same fourteen headings in the same order: title and description; programme and status; preregistration; preprint; publication; repository contents; data availability; reproducing the analysis; ethics and governance; funding and partners; authors and contributions; licences; how to cite; related repositories. Empty headings say "none" or "not applicable" rather than being deleted.

## 9. Releases and Zenodo

Tags follow `vMAJOR.MINOR.PATCH`:

- `v0.x.y` while the study is in development
- `v1.0.0` at manuscript submission
- `v1.x.0` at each resubmission
- `v2.0.0` at acceptance or publication

Every `v1.0.0` and later tag is a GitHub Release, which Zenodo archives automatically once the repository is connected. Zenodo issues a concept DOI (all versions) and a version DOI (that release). Manuscripts cite the version DOI. `CITATION.cff` and `CHANGELOG.md` are updated before every release.

## 10. Licences

Code (`code/`): PolyForm Noncommercial 1.0.0, in `LICENSE-code.md`.
Everything else: CC BY-NC 4.0, in `LICENSE-materials.md`.
Copyright holder: Erasmus University Rotterdam. Commercial licences on request via gamblingresearch@essb.eur.nl. Individual files may carry a more permissive licence if stated in the file.

## 11. Ownership and access

The organisation is owned by the project account (gamblingresearch@essb.eur.nl) and at least two named owners. Members get read access by default and write access per repository. Two-factor authentication is required for everyone.

## 12. Commit messages

One line, imperative, saying what changed: "Add gitignore", "Rename docs to protocol", "Fix table 4 numbering".
