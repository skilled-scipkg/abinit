# abinit source map: Theory and Methods

Generated from source roots:
- `shared`
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<bse|exciton|haydock|harmonics|pseudopotential|berry|mbpt>" src/71_bse src/78_effpot src/64_psp src/67_common shared/common/src/28_numeric_noabirule`
- `rg -n "subroutine|function|module" src/71_bse src/78_effpot src/64_psp src/67_common shared/common/src/28_numeric_noabirule`

## Suggested source entry points (function-level)
- `src/71_bse/m_hexc.F90` | BSE Hamiltonian/excitonic kernel setup.
- `src/71_bse/m_exc_build.F90` | excitonic matrix assembly.
- `src/71_bse/m_exc_diago.F90` | excitonic diagonalization path.
- `src/71_bse/m_exc_spectra.F90` | spectra construction from BSE states.
- `src/71_bse/m_haydock.F90` | Haydock recursion implementation.
- `src/71_bse/m_haydock_io.F90` | Haydock input/output handling.
- `src/78_effpot/m_harmonics_terms.F90` | spherical/anharmonic term handling.
- `src/64_psp/m_psp8.F90` | pseudopotential format behavior.
- `src/67_common/m_berryphase_new.F90` | Berry-phase method implementation.
- `shared/common/src/28_numeric_noabirule/m_numeric_tools.F90` | low-level numerical kernels used by methods.
