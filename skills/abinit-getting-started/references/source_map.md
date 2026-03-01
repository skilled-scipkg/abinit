# abinit source map: Getting Started

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<input|dataset|parse|scf|psp|output>" src/57_iovars src/64_psp src/95_drive src/98_main`
- `rg -n "subroutine|function|module" src/57_iovars src/64_psp src/95_drive src/98_main`

## Suggested source entry points (function-level)
- `src/98_main/abinit.F90` | main program entry and top-level execution handoff.
- `src/95_drive/m_driver.F90` | workflow dispatch by run mode/optdriver.
- `src/95_drive/m_gstate.F90` | ground-state SCF driver loop.
- `src/57_iovars/m_invars1.F90` | primary input variable parsing.
- `src/57_iovars/m_invars2.F90` | secondary variable parsing and checks.
- `src/57_iovars/m_chkinp.F90` | input consistency validation.
- `src/57_iovars/m_outvars.F90` | output variable reporting.
- `src/64_psp/m_pspini.F90` | pseudopotential initialization.
- `src/64_psp/m_psps.F90` | pseudopotential data handling.
- `src/57_iovars/m_mpi_setup.F90` | runtime MPI setup defaults.
