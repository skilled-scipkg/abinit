# abinit source map: Parallel and HPC

Generated from source roots:
- `cmake`
- `shared`
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<mpi|openmp|gpu|paral|scheduler|fft>" cmake src/52_fft_mpi_noabirule src/57_iovars src/72_response src/79_seqpar_mpi src/66_nonlocal shared/common/src/17_gpu_toolbox`
- `rg -n "subroutine|function|module|function\(" cmake src/52_fft_mpi_noabirule src/57_iovars src/72_response src/79_seqpar_mpi src/66_nonlocal`

## Suggested source entry points (function-level)
- `src/57_iovars/m_mpi_setup.F90` | MPI communicator/setup controls.
- `src/52_fft_mpi_noabirule/m_fftcore.F90` | MPI FFT decomposition behavior.
- `src/72_response/m_paral_pert.F90` | DFPT parallel perturbation distribution.
- `src/79_seqpar_mpi/m_wvl_wfsinp.F90` | wavelet parallel wavefunction handling.
- `src/79_seqpar_mpi/m_lobpcgwf.F90` | parallel eigensolver workflow.
- `src/79_seqpar_mpi/m_tddft.F90` | parallel TDDFT path.
- `src/66_nonlocal/m_gemm_nonlop_gpu.F90` | GPU nonlocal projector kernels.
- `shared/common/src/17_gpu_toolbox/cuda_api_error_check.h` | CUDA error handling wrappers.
- `shared/common/src/17_gpu_toolbox/hip_api_error_check.h` | HIP error handling wrappers.
- `cmake/get_mpi_vendor.cmake` | MPI vendor detection logic.
- `cmake/manage_openmp_target.cmake` | OpenMP target/offload wiring.
- `cmake/try_compile/have_openmp_offload.F90` | OpenMP offload feature probe.
- `src/98_main/fold2Bloch.F90` | parallel postprocessing executable path.
