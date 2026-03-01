# abinit source map: Variables

Generated from source roots:
- `abimkdocs`
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<variable|varset|efield|diel|bec|parser>" abimkdocs src/57_iovars src/44_abitypes_defs src/65_paw src/77_ddb`
- `rg -n "def |subroutine|function|module" abimkdocs src/57_iovars src/44_abitypes_defs src/65_paw src/77_ddb`

## Suggested source entry points (function-level)
- `abimkdocs/variables.py` | variable object model and registry helpers.
- `abimkdocs/variables_abinit.py` | ABINIT variable definitions.
- `abimkdocs/variables_anaddb.py` | anaddb variable definitions.
- `abimkdocs/variables_optic.py` | optic variable definitions.
- `src/57_iovars/m_invars1.F90` | input variable parsing path 1.
- `src/57_iovars/m_invars2.F90` | input variable parsing path 2.
- `src/57_iovars/m_chkinp.F90` | variable consistency checks.
- `src/44_abitypes_defs/m_efield.F90` | electric-field datatype/runtime use.
- `src/65_paw/m_paw_efield.F90` | PAW electric-field variable behavior.
- `src/77_ddb/m_ddb_diel.F90` | dielectric/BEC-related post-processing behavior.
