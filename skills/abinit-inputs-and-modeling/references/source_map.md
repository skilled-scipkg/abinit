# abinit source map: Inputs and Modeling

Generated from source roots:
- `abimkdocs`
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<variable|dataset|kpt|pseudo|symmetry|dfpt>" src/57_iovars src/64_psp src/41_geometry src/72_response abimkdocs`
- `rg -n "subroutine|function|module|def" src/57_iovars src/64_psp src/41_geometry src/72_response abimkdocs`

## Suggested source entry points (function-level)
- `src/57_iovars/m_invars1.F90` | core input variable parsing.
- `src/57_iovars/m_invars2.F90` | variable defaults/extended parsing.
- `src/57_iovars/m_chkinp.F90` | consistency and sanity checks.
- `src/57_iovars/m_inkpts.F90` | k-point input parsing and setup.
- `src/41_geometry/m_spgdata.F90` | space-group and symmetry data.
- `src/64_psp/m_pspini.F90` | pseudo initialization checks.
- `src/64_psp/m_psps.F90` | pseudo file data structures.
- `src/64_psp/m_psp8.F90` | PSP8 parser behavior.
- `src/72_response/m_paral_pert.F90` | DFPT perturbation scheduling.
- `src/95_drive/m_gstate.F90` | SCF behavior used by many models.
- `abimkdocs/variables_abinit.py` | canonical variable metadata.
- `abimkdocs/variables.py` | variable database plumbing.
