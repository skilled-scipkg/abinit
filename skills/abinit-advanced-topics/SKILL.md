---
name: abinit-advanced-topics
description: Use this skill for low-frequency ABINIT topics consolidated from single-doc skills (about, legacy, maintainers, spacegroup, todo, external resources).
---

# abinit: Advanced Topics

## Scope
- Handle low-frequency, single-doc topics that do not justify dedicated standalone skills.
- Keep routing explicit so common workflows still go to high-signal skills.

## Route the request
- Route to `abinit-troubleshooting` for runtime/build failure diagnosis.
- Route to `abinit-inputs-and-modeling` for variable/method/model setup.
- Route to `abinit-build-and-install` for installation and dependency concerns.
- Stay in this skill for:
  - license and project meta pages,
  - legacy tuning notes,
  - maintainer statistics,
  - spacegroup reference list,
  - documentation TODO and external resources pages.

## Primary documentation references
- `doc/about/license.md`
- `doc/guide/legacy/tuning.txt`
- `doc/maintainers/statistics.txt`
- `doc/guide/spacegroup.md`
- `doc/TODO.md`
- `doc/topics/external_resources.md`

## Workflow
- Start from the exact page above matching the question.
- If details are missing, inspect `references/doc_map.md` for combined inventory context.
- Escalate to `references/source_map.md` only when implementation-level details are requested.
- Cite exact file paths.

## Optional deeper inspection
- `abimkdocs`
- `abimkdocs_plugin`
- `scripts`
- `src`

## Source entry points for unresolved issues
- `scripts/post_processing/appa/gui/about.py`
- `src/41_geometry/m_spgdata.F90`
- `abimkdocs/variables.py`
- `abimkdocs_plugin/__init__.py`
- `cmake/abinit_install.cmake`
- `src/98_main/abinit.F90`
- Prefer targeted search (for example: `rg -n "<symbol_or_keyword>" scripts src abimkdocs abimkdocs_plugin cmake`).
