---
name: abinit-troubleshooting
description: Use this skill for symptom-driven ABINIT diagnostics across build/runtime/test failures, with fast repro and checkpoint commands.
---

# abinit: Troubleshooting

## High-Signal Playbook

### Route conditions
- Route to `abinit-build-and-install` for unresolved configure/link/dependency setup issues.
- Route to `abinit-tests` when the main issue is test harness selection/comparison.
- Route to `abinit-parallel-hpc` for scale-only regressions and launcher tuning.

### Triage questions
- Which phase fails: startup, SCF/runtime, post-processing, or tests?
- Is the failure deterministic or intermittent?
- Does it reproduce on a known tutorial input?
- Are there hardware/compiler-specific signals (MPI/GPU/OpenMP)?
- What is the first fatal message in the log?

### Canonical workflow
1. Reproduce with a minimal known input in a clean working directory.
2. Capture full logs (`stdout` and `stderr`) and scan for first fatal marker.
3. Check build/runtime feature report (`abinit -b`).
4. Cross-check known issues docs.
5. Run a minimal regression subset to classify scope.
6. Escalate to source map for function-level diagnostics.

### Minimal working examples
```sh
# Runtime feature snapshot
abinit -b
```

```sh
# Minimal reproduction and log scan
export ABI_PSPDIR="$PWD/tests/Pspdir"
abinit tests/tutorial/Input/tbase2_1.abi > repro.log 2>&1
grep -niE "error|warning|failed|abort" repro.log
```

```sh
# Harness-level sanity
cd tests
./runtests.py --keywords MINIMAL --yaml-simplified-diff
```

### Pitfalls and fixes
- Debugging from partial logs: always keep full command + environment + complete log.
- Chasing downstream errors instead of the first fatal condition.
- Mixing stale restart files/config artifacts between repro attempts.
- Ignoring known platform/compiler caveats in `KNOWN_PROBLEMS`.

### Validation checkpoints
- Reproduction is stable with an explicit command/input/log triplet.
- First-failure signature is identified and categorized.
- Fix candidate removes the original fatal signature.
- Minimal regression subset remains clean after fix.

## Scope
- Handle practical diagnostics for ABINIT failures and regressions.
- Prioritize short, reproducible loops before deep source dives.

## Primary documentation references
- `KNOWN_PROBLEMS`
- `doc/faq/tuning_abinit.md`
- `doc/faq/Troubleshooting.md`
- `doc/faq/configuration_and_compilation.md`
- `tests/README.md`

## Workflow
- Start from symptom + minimal repro command.
- Use `references/doc_map.md` for related troubleshooting docs.
- Confirm whether issue is setup, runtime, or harness-specific.
- Escalate to `references/source_map.md` for function-level checks.
- Cite exact paths, commands, and first-failure log lines.

## Tutorials and examples
- `tests/tutorial/Input/tbase2_1.abi`
- `tests/tutoparal/Input/tdfpt_01.abi`
- `tests/runtests.py`

## Test references
- `tests/runtests.py`
- `tests/pymods/fldiff.py`
- `tests/pymods/testsuite.py`

## Optional deeper inspection
- `shared/common/src/16_hideleave`
- `shared/common/src/17_gpu_toolbox`
- `src/57_iovars`
- `src/95_drive`
- `cmake`

## Source entry points for unresolved issues
- `shared/common/src/16_hideleave/m_errors.F90`
- `shared/common/src/17_gpu_toolbox/cuda_api_error_check.h`
- `shared/common/src/17_gpu_toolbox/hip_api_error_check.h`
- `src/57_iovars/m_chkinp.F90`
- `src/57_iovars/m_mpi_setup.F90`
- `src/95_drive/m_driver.F90`
- `cmake/compiler_setup.cmake`
- Prefer targeted search (for example: `rg -n "<symbol_or_keyword>" shared/common/src/16_hideleave shared/common/src/17_gpu_toolbox src/57_iovars src/95_drive cmake`).
