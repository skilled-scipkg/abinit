---
name: abinit-developer-guide
description: Use this skill for ABINIT contribution workflow, source-tree conventions, docs generation, and test-gated development changes.
---

# abinit: Developer Guide

## High-Signal Playbook

### Route conditions
- Route to `abinit-tests` for detailed test selection/debugging commands.
- Route to `abinit-build-and-install` for dependency/compiler setup issues.
- Route to `abinit-inputs-and-modeling` when user requests method/input advice instead of contribution mechanics.

### Triage questions
- Is the change in Fortran source, build system, docs, tests, or variable database?
- Is this a quick bugfix or feature development with new interfaces?
- Does the change require new input variables or docs pages?
- Which suites must pass before merge?
- Are `abinit.src`/CMake declarations updated for new files?
- Is local doc generation required (`mksite.py` path)?

### Canonical workflow
1. Sync branch and run baseline tests before editing.
2. Implement source changes, updating directory `abinit.src` entries for new files.
3. Rebuild (`config/scripts/makemake` + configure/make, or CMake equivalent).
4. Add/adjust tests with valid TEST_INFO metadata.
5. Update docs and variable database (`abimkdocs/variables_*.py`) when interfaces change.
6. Run targeted tests and at least one smoke suite.
7. Prepare merge request with reproducible commands and changed-path rationale.

### Minimal working example
```sh
# Typical local dev loop
./config/scripts/makemake
mkdir -p build-dev && cd build-dev
../configure FC=gfortran
make -j4
cd ../tests
./runtests.py fast -j2
```

```sh
# Docs preview loop for developer docs/variables changes
pip install -r requirements.txt
./mksite.py serve --dirtyreload
```

### Pitfalls and fixes
- New source file not registered: update local `abinit.src` (and matching build metadata where needed).
- Skipping regression checks after refactors: rerun targeted + smoke suites.
- Updating variable semantics only in prose docs: keep `abimkdocs/variables_*.py` in sync.
- Expecting live-reload to pick up generated topic/variable artifacts automatically: restart full site generation when required (`doc/developers/abimkdocs.md`).
- Submitting semantic changes without new/updated tests.

### Convergence and validation checks
- Build succeeds from a clean directory with intended compiler/toolchain.
- Targeted tests for changed code paths pass.
- Smoke suite remains green after change.
- Documentation generation succeeds when docs/variables were touched.

## Scope
- Handle architecture-level development workflow, contribution rules, and maintenance practices.
- Keep recommendations practical and aligned with ABINIT project conventions.

## Primary documentation references
- `doc/developers/overview_development.md`
- `doc/developers/git_and_gitlab.md`
- `doc/developers/developers_howto.md`
- `doc/developers/testsuite_howto.md`
- `doc/developers/abimkdocs.md`
- `doc/developers/markdown.md`
- `doc/maintainers/check_list.txt`
- `doc/about/contributing.md`

## Workflow
- Start from developer policy/docs, then run tests/build loops.
- Use `references/doc_map.md` for the full developer-doc inventory.
- Escalate to source maps for exact implementation points.
- Always cite changed files and test commands.

## Tutorials and examples
- `doc/developers`
- `tests/tutorial/Input`

## Test references
- `tests/runtests.py`
- `tests/pymods/testsuite.py`

## Optional deeper inspection
- `abimkdocs`
- `abimkdocs_plugin`
- `config`
- `src`

## Source entry points for unresolved issues
- `config/scripts/makemake`
- `configure.ac`
- `CMakeLists.txt`
- `src/57_iovars/abinit.src`
- `src/95_drive/abinit.src`
- `tests/runtests.py`
- `tests/pymods/testsuite.py`
- `abimkdocs/variables_abinit.py`
- `abimkdocs/abi_check.py`
- `abimkdocs_plugin/__init__.py`
- `mksite.py`
- Prefer targeted search (for example: `rg -n "<symbol_or_keyword>" config src tests abimkdocs`).
