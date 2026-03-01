# abinit source map: Tests

Generated from source roots:
- `src`
- `tests`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<suite|keyword|yaml|diff|runner|rerun|mpi>" tests/runtests.py tests/pymods src/95_drive src/57_iovars`
- `rg -n "def |class |subroutine|function|module" tests/runtests.py tests/pymods src/95_drive src/57_iovars`

## Suggested source entry points (function-level)
- `tests/runtests.py` | top-level CLI and suite selection.
- `tests/pymods/testsuite.py` | suite model and execution pipeline.
- `tests/pymods/jobrunner.py` | job launch/retry behavior.
- `tests/pymods/fldiff.py` | numeric/text diff logic.
- `tests/pymods/yaml_tools/tester.py` | YAML-based regression comparator.
- `tests/pymods/yaml_tools/conf_parser.py` | YAML config parsing and validation.
- `tests/pymods/devtools.py` | developer test utilities.
- `tests/pymods/subprocesswithtimeout.py` | timeout/process handling.
- `src/95_drive/m_unittests.F90` | in-code unit-test entrypoints.
- `src/57_iovars/m_mpi_setup.F90` | MPI setup behavior affecting test runs.
