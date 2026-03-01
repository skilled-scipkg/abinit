---
name: abinit-tests
description: Use this skill for ABINIT regression/integration test execution, selection, authoring conventions, and failure triage via runtests.py.
---

# abinit: Tests

## High-Signal Playbook

### Route conditions
- Route to `abinit-build-and-install` if binaries are missing or not linkable.
- Route to `abinit-troubleshooting` when failures are runtime/compiler/platform-specific rather than test-harness usage.
- Route to `abinit-developer-guide` for contribution workflow and merge-readiness.

### Triage questions
- Is the goal smoke validation, targeted regression, or full-suite execution?
- Which executable/suite/keyword should be selected (`fast`, `v*`, `paral`, tutorial suites)?
- Are MPI/OpenMP resources explicitly required?
- Is failure reproducible or intermittent?
- Is this a new test addition or a debugging run of existing tests?
- Are reference diffs semantic (`yaml`) or strict line-by-line expectations?

### Canonical workflow
1. Start in `tests/` and inspect available options (`./runtests.py --help`).
2. Run a dry listing first (`-d` / `-l`) for selected suites.
3. Execute smoke subset (`make check` or `./runtests.py --keywords MINIMAL --yaml-simplified-diff`).
4. Run targeted suites/keywords (`./runtests.py v1 -k abinit`, slicing as needed).
5. For MPI tests, specify processors (`-n`) and launcher config (`-c mpi.cfg`) if needed.
6. Re-run failed set only (`--rerun=failed`) after fixes.
7. For new tests, enforce naming/TEST_INFO conventions from `doc/developers/testsuite_howto.md`.

### Minimal working example
```sh
cd tests
./runtests.py -d fast
./runtests.py fast -j2
./runtests.py v1 -k abinit
./runtests.py --rerun=failed
```

```sh
# MPI-focused example
cd tests
./runtests.py -n 4 paral
```

### Pitfalls and fixes
- Treating test inputs as fully converged production settings: many tests are intentionally underconverged (`tests/README.md`).
- Mis-specified TEST_INFO (`max_nprocs`, chain metadata, tolerances): validate with documented conventions.
- Wrong suite/file naming conventions (`tNN.in` or `tsubsuite_N.in`).
- Running stale cached metadata (`--use-cache`) while branch changed.
- Ignoring launcher specifics for MPI environments; use `-c` config file when defaults fail.
- Comparing wrong artifacts: use simplified yaml diff where appropriate.

### Convergence and validation checks
- Smoke suite passes cleanly (`make check` / MINIMAL keywords).
- No unresolved failures remain after `--rerun=failed`.
- Parallel tests run within declared `max_nprocs` bounds.
- New tests include reproducible TEST_INFO metadata and tolerances.

## Scope
- Handle execution, selection, debugging, and authoring of ABINIT tests.
- Prioritize reproducible, minimal feedback loops.

## Primary documentation references
- `tests/README.md`
- `tests/runtests.py`
- `doc/developers/testsuite_howto.md`
- `KNOWN_PROBLEMS`
- `tests/Pspdir/Psdj_nc_sr_04_pw_std_psp8/README.md`
- `tests/Pspdir/Psdj_paw_pw_std/README.md`

## Workflow
- Start with `tests/README.md` and `runtests.py --help`.
- Use `references/doc_map.md` for full test-related file inventory.
- Prefer targeted suite/keyword runs before full sweeps.
- Escalate to source maps when harness internals or comparison logic must be inspected.
- Cite exact test/doc paths and command invocations.

## Tutorials and examples
- `tests/tutorial/Input`
- `tests/tutoparal/Input`
- `tests/tutorespfn/Input`

## Test references
- `tests/runtests.py`
- `tests/pymods/testsuite.py`
- `tests/pymods/jobrunner.py`

## Optional deeper inspection
- `tests/pymods`
- `src/95_drive`

## Source entry points for unresolved issues
- `tests/runtests.py`
- `tests/pymods/testsuite.py`
- `tests/pymods/jobrunner.py`
- `tests/pymods/fldiff.py`
- `tests/pymods/yaml_tools/tester.py`
- `tests/__init__.py`
- `tests/fast/__init__.py`
- `src/95_drive/m_unittests.F90`
- `src/57_iovars/m_mpi_setup.F90`
- Prefer targeted search (for example: `rg -n "<symbol_or_keyword>" tests/runtests.py tests/pymods src/95_drive`).
