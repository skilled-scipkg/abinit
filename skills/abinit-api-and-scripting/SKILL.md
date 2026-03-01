---
name: abinit-api-and-scripting
description: Use this skill for ABINIT programmatic interfaces, YAML/testing APIs, bindings, and scripting-based automation around simulations.
---

# abinit: API and Scripting

## High-Signal Playbook

### Route conditions
- Route to `abinit-inputs-and-modeling` for physics/input-parameter choices.
- Route to `abinit-analysis-and-output` for interpretation of generated results.
- Route to `abinit-build-and-install` if bindings or tools fail at configure/build time.

### Triage questions
- Is the user automating run submission, parsing outputs, or using external bindings?
- Is the target interface Fortran internals, Python tooling, or command-line utilities?
- Does the workflow depend on YAML-based regression outputs?
- Is `cut3d`/post-processing needed in the automation chain?

### Canonical workflow
1. Pick the interface layer (ABINIT executable chain, YAML tools, or bindings).
2. Start from a known test/tutorial input and run one deterministic baseline job.
3. Add parser/post-processing script execution.
4. Validate that scripted outputs match expected files/sections.
5. Escalate to `references/source_map.md` for API function-level tracing.

### Minimal working examples
```sh
# Inspect YAML test API surface
python tests/pymods/yaml_tools/tester.py --help
```

```sh
# Generate a reproducible output for scripted post-processing
export ABI_PSPDIR="$PWD/tests/Pspdir"
abinit tests/tutorespfn/Input/toptic_1.abi > toptic_1.log
python scripts/post_processing/plot_bandstructure.py --help
```

### Pitfalls and fixes
- Scripting against unstable filenames: rely on explicit prefixes and known output conventions.
- Mixing parser logic for different output families (`.abo`, YAML, NetCDF) without format checks.
- Assuming bindings are built by default; verify configure/build flags first.
- Treating tutorial scripts as production-hardened pipelines without validation.

### Validation checkpoints
- Script runs produce no traceback/segfault.
- Parsed quantities match expected values/trends from tutorial references.
- YAML tooling can parse and compare at least one baseline case.
- Interface-specific dependencies are explicitly detected during build.

## Scope
- Handle automation hooks, bindings, YAML/test APIs, and scripting-based run orchestration.
- Keep guidance reproducible with repository-contained examples.

## Primary documentation references
- `doc/developers/yaml_tools_api.md`
- `doc/developers/new_testsuite.md`
- `doc/developers/psp8_info.md`
- `doc/tutorial/cut3d.md`
- `doc/tutorial/nlo.md`
- `tests/tutorespfn/TutoNLO/summary_NLO.txt`

## Workflow
- Start from docs and tutorial examples for the target interface.
- Use `references/doc_map.md` for broader API/scripting inventory.
- Validate scripts on known test inputs before adapting to production studies.
- Escalate to `references/source_map.md` for function-level behavior checks.
- Cite exact file paths and commands.

## Tutorials and examples
- `tests/tutorespfn/Input/toptic_1.abi`
- `tests/tutorespfn/Input/tnlo_1.abi`
- `tests/tutoplugs/Input/tw90_1.abi`
- `scripts/post_processing/plot_bandstructure.py`

## Test references
- `tests/pymods/yaml_tools/tester.py`
- `tests/pymods/yaml_tools/conf_parser.py`
- `tests/runtests.py`

## Optional deeper inspection
- `bindings`
- `scripts/post_processing`
- `shared/common/src/17_yaml_out`
- `src/67_python_invocation_ext`

## Source entry points for unresolved issues
- `src/98_main/cut3d.F90`
- `src/95_drive/m_cut3d.F90`
- `src/67_python_invocation_ext/m_invocation_tools.F90`
- `shared/common/src/17_yaml_out/m_yaml.F90`
- `tests/pymods/yaml_tools/tester.py`
- `bindings/configure.ac`
- Prefer targeted search (for example: `rg -n "<symbol_or_keyword>" src/67_python_invocation_ext src/95_drive src/98_main shared/common/src/17_yaml_out bindings tests/pymods scripts`).
