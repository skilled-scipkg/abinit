# abinit source map: Developer Guide

Generated from source roots:
- `abimkdocs`
- `abimkdocs_plugin`
- `config`
- `src`
- `tests`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<new file|abinit.src|testsuite|variables|docs>" config src tests abimkdocs abimkdocs_plugin mksite.py`
- `rg -n "subroutine|function|module|class|def" src tests/pymods abimkdocs abimkdocs_plugin`

## Suggested source entry points (function-level)
- `config/scripts/makemake` | regenerates make/config files after source-tree edits.
- `configure.ac` | developer-facing configure checks and options.
- `CMakeLists.txt` | top-level CMake dependency/target graph.
- `src/57_iovars/abinit.src` | source registration for iovars files.
- `src/95_drive/abinit.src` | source registration for driver files.
- `tests/runtests.py` | test orchestration entrypoint.
- `tests/pymods/testsuite.py` | suite definition/execution behavior.
- `abimkdocs/variables_abinit.py` | variable database content and metadata.
- `abimkdocs/abi_check.py` | documentation/metadata checks.
- `abimkdocs_plugin/__init__.py` | MkDocs plugin hook registration.
- `mksite.py` | local docs build/serve orchestration.
