---
name: abinit-parallel-hpc
description: Use this skill for MPI/OpenMP/GPU execution patterns, scaling diagnostics, and scheduler-facing ABINIT runs.
---

# abinit: Parallel and HPC

## High-Signal Playbook

### Route conditions
- Route to `abinit-build-and-install` for missing MPI/OpenMP/GPU build features.
- Route to `abinit-troubleshooting` for platform/compiler crashes not specific to parallel decomposition.
- Route to `abinit-inputs-and-modeling` for method/input correctness issues.

### Triage questions
- Is the run MPI-only, hybrid MPI+OpenMP, or GPU-offloaded?
- Which launcher and scheduler are required (`mpirun`, `srun`, batch script)?
- Which decomposition is targeted (`k`/`band`/`pw`/image)?
- Is the goal throughput, strong scaling, or weak scaling?
- Which stage regresses under scale (SCF, FFT, I/O, response)?

### Canonical workflow
1. Verify build capabilities (`abinit -b`, compiler/MPI stack, OpenMP flags).
2. Reproduce with a known parallel tutorial input (`tests/tutoparal/Input/tparal_bandpw_01.abi` or `tdfpt_01.abi`).
3. Run one fixed-size baseline, then scale processor counts.
4. Capture timing and parallel diagnostics from logs.
5. Change one decomposition control at a time.
6. Escalate to `references/source_map.md` for module-level bottlenecks.

### Minimal working examples
```sh
export ABI_PSPDIR="$PWD/tests/Pspdir"
mpirun -n 4 abinit tests/tutoparal/Input/tparal_bandpw_01.abi > tparal_bandpw_01.log
```

```sh
# DFPT-oriented parallel smoke
export ABI_PSPDIR="$PWD/tests/Pspdir"
mpirun -n 8 abinit tests/tutoparal/Input/tdfpt_01.abi > tdfpt_01.log
```

### Pitfalls and fixes
- Comparing scaled runs with different physics settings: keep inputs identical for scaling studies.
- Oversubscribed ranks/threads: pin resources explicitly and validate `OMP_NUM_THREADS`.
- Ignoring I/O contention: separate compute and filesystem bottlenecks.
- Assuming GPU path is active without verifying compile/runtime capability reports.

### Validation checkpoints
- Parallel run completes with no deadlock/hang and no fatal MPI errors.
- Reported wall time improves or degrades predictably with rank count.
- Physical observables remain consistent across decomposition choices.
- Timing sections identify a dominant hotspot before deeper tuning.

## Scope
- Handle MPI/OpenMP/GPU execution, scaling, and launcher patterns.
- Keep recommendations runnable with tutorial-grade inputs before production adaptation.

## Primary documentation references
- `doc/tutorial/basepar.md`
- `doc/tutorial/paral_bandpw.md`
- `doc/tutorial/paral_mbt.md`
- `doc/tutorial/paral_images.md`
- `doc/tutorial/paral_gswvl.md`
- `doc/tutorial/paral_dfpt.md`
- `doc/developers/mpi_devtools.md`
- `doc/guide/fold2bloch.md`

## Workflow
- Start with tutorial/doc guidance matching the parallel mode.
- Use `references/doc_map.md` for full parallel/HPC doc inventory.
- Run known tutorial inputs before tuning production jobs.
- Escalate to `references/source_map.md` for function-level bottleneck tracing.
- Cite exact file paths and launch commands.

## Tutorials and examples
- `tests/tutoparal/Input/tparal_bandpw_01.abi`
- `tests/tutoparal/Input/tdfpt_01.abi`
- `tests/tutoparal/Input/timages_01.abi`
- `tests/tutoparal/Input/tmbt_1.abi`

## Test references
- `tests/paral`
- `tests/hpc`
- `tests/runtests.py`

## Optional deeper inspection
- `cmake`
- `shared/common/src/17_gpu_toolbox`
- `src/52_fft_mpi_noabirule`
- `src/79_seqpar_mpi`

## Source entry points for unresolved issues
- `src/57_iovars/m_mpi_setup.F90`
- `src/52_fft_mpi_noabirule/m_fftcore.F90`
- `src/72_response/m_paral_pert.F90`
- `src/79_seqpar_mpi/m_wvl_wfsinp.F90`
- `src/79_seqpar_mpi/m_lobpcgwf.F90`
- `src/66_nonlocal/m_gemm_nonlop_gpu.F90`
- `cmake/get_mpi_vendor.cmake`
- `cmake/manage_openmp_target.cmake`
- Prefer targeted search (for example: `rg -n "<symbol_or_keyword>" src/79_seqpar_mpi src/52_fft_mpi_noabirule src/57_iovars cmake shared/common/src/17_gpu_toolbox`).
