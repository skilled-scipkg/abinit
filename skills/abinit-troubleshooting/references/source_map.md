# abinit source map: Troubleshooting

Generated from source roots:
- `cmake`
- `shared`
- `src`
- `tests/pymods`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<error|warning|abort|mpi|gpu|configure|dependency>" src/57_iovars src/95_drive src/98_main shared/common/src/16_hideleave shared/common/src/17_gpu_toolbox cmake tests/pymods`
- `rg -n "subroutine|function|module|ERROR|WARN|die" src/57_iovars src/95_drive src/98_main shared/common/src/16_hideleave shared/common/src/17_gpu_toolbox`

## Suggested source entry points (function-level)
- `shared/common/src/16_hideleave/m_errors.F90` | central ABINIT error/abort handlers.
- `shared/common/src/17_gpu_toolbox/cuda_api_error_check.h` | CUDA call diagnostics.
- `shared/common/src/17_gpu_toolbox/hip_api_error_check.h` | HIP call diagnostics.
- `src/57_iovars/m_chkinp.F90` | input sanity checks and common failure messages.
- `src/57_iovars/m_mpi_setup.F90` | MPI startup failures and communicator checks.
- `src/95_drive/m_driver.F90` | top-level runtime failure branching.
- `src/98_main/abinit.F90` | startup/argument failure paths.
- `cmake/compiler_setup.cmake` | compiler capability failure points.
- `cmake/options.cmake` | misconfigured build options diagnostics.
- `cmake/scalapack_setup.cmake` | ScaLAPACK detection/link diagnostics.
- `tests/pymods/fldiff.py` | output-diff diagnostics for regression failures.
