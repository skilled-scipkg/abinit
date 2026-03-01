# abinit source map: Simulation Workflows

Generated from source roots:
- `cmake`
- `shared`
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<driver|restart|dataset|state|cut3d|wannier|timing|dynamics>" src/95_drive src/98_main src/71_wannier src/78_effpot shared/common/src/18_timing cmake`
- `rg -n "subroutine|function|module|function\(" src/95_drive src/98_main src/71_wannier src/78_effpot shared/common/src/18_timing cmake`

## Suggested source entry points (function-level)
- `src/98_main/abinit.F90` | main runtime entry for standard simulations.
- `src/95_drive/m_driver.F90` | global run dispatch and dataset flow.
- `src/95_drive/m_gstate.F90` | GS loop and convergence flow.
- `src/95_drive/m_dfpt_looppert.F90` | DFPT multi-perturbation workflow.
- `src/95_drive/m_gstateimg.F90` | image/string-method workflow support.
- `src/95_drive/m_cut3d.F90` | cut3d run-stage orchestration.
- `src/98_main/cut3d.F90` | cut3d executable entrypoint.
- `src/71_wannier/defs_wannier90.F90` | Wannier90 interface structures.
- `cmake/build_or_find_wannier90.cmake` | Wannier dependency resolution.
- `src/78_effpot/m_slc_dynamics.F90` | lattice/spin dynamics workflow hooks.
- `shared/common/src/18_timing/m_time.F90` | timing/checkpoint instrumentation.
