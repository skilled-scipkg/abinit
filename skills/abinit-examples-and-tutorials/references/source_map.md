# abinit source map: Examples and Tutorials

Generated from source roots:
- `abimkdocs`
- `scripts`
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<tutorial_method|optic|dftu|positron|dfpt|lruj>" src/67_common src/68_dmft src/95_drive src/98_main abimkdocs scripts/post_processing`
- `rg -n "subroutine|function|module|class|def" src/67_common src/68_dmft src/95_drive src/98_main abimkdocs scripts/post_processing`

## Suggested source entry points (function-level)
- `abimkdocs/variables_optic.py` | variable docs used by optics tutorials.
- `src/98_main/optic.F90` | optics executable path and argument handling.
- `src/98_main/lruj.F90` | linear-response U/J executable entry.
- `src/68_dmft/m_dftu_self.F90` | DFT+U self-consistency behavior.
- `src/67_common/m_optic_tools.F90` | optics helper routines.
- `src/67_common/m_positron.F90` | positron-related method routines.
- `src/67_common/m_nucprop.F90` | near-nucleus observable routines.
- `src/95_drive/m_dfpt_looppert.F90` | DFPT perturbation loop flow.
- `src/71_wannier/m_wannier_builder.F90` | Wannier construction routines.
- `scripts/post_processing/ab2epw_quad.py` | quadrupole/e-ph post-processing glue.
