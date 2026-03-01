---
name: abinit-inputs-and-modeling
description: Use this skill for ABINIT input-variable interpretation, physical-model setup (structure/pseudos/cutoffs), and convergence-critical modeling decisions.
---

# abinit: Inputs and Modeling

## High-Signal Playbook

### Route conditions
- Route to `abinit-getting-started` for first-run basics and package orientation.
- Route to `abinit-examples-and-tutorials` when a method walkthrough is preferable to variable-by-variable advice.
- Route to `abinit-api-and-scripting` for scripted input generation or post-processing automation.
- Route to `abinit-parallel-hpc` for parallel decomposition/performance tuning.

### Triage questions
- Which method family is targeted (`ground-state`, `relaxation`, `DFPT`, `GW`, `PAW`, etc.)?
- What observable is required (energy, forces, phonons, dielectric response, band gap, ...)?
- Which pseudopotential type is used and from where?
- What are current convergence controls (`ecut`, `ngkpt`, `nstep`, tolerance variables)?
- Is symmetry/k-point setup explicit and physically consistent?
- Are there restart artifacts or inconsistent dataset settings?

### Canonical workflow
1. Build the input skeleton from `doc/topics/_GSintroduction.md` (structure, species, basis, k-grid, SCF controls).
2. Validate atom typing and pseudopotential compatibility (`ntypat`, `typat`, `znucl`, pseudo files).
3. Add method controls (`geoopt`/`moldyn`/`optdriver`/`rfphon`/`rfelfd`) according to target observable.
4. Set convergence knobs and stopping criteria (`ecut`, `ngkpt`, `nstep`, `tolvrs`/`toldfe`, `tolmxf`).
5. Run small validation jobs first, then sweep dominant convergence parameters.
6. Cross-check variable meaning in docs (`varset:*`) and in `abimkdocs/variables_abinit.py` when needed.
7. Promote to production only after stability checks on target quantities.

### Minimal working example
```abinit
# Compact GS input model (Al, periodic)
acell 3*7.56
rprim 0 .5 .5  .5 0 .5  .5 .5 0
ntypat 1
znucl 13
natom 1
typat 1
xred 0 0 0
pp_dirpath "$ABI_PSPDIR"
pseudos "Psdj_nc_sr_04_pw_std_psp8/Al.psp8"
ecut 10
ngkpt 8 8 8
nshiftk 4
shiftk 0.5 0.5 0.5
       0.5 0.0 0.0
       0.0 0.5 0.0
       0.0 0.0 0.5
nstep 20
occopt 4
tolvrs 1.0d-18
```

```sh
export ABI_PSPDIR="$PWD/tests/Pspdir"
abinit model.abi > model.log
```

### Pitfalls and fixes
- Using test pseudopotentials in production: replace with recommended data tables (`doc/guide/new_user.md`).
- Forgetting PAW fine-grid controls: set/check `pawecutdg` where relevant.
- Relying on loose tutorial tolerances: tighten for publication-grade numbers.
- Inconsistent k-point/smearing choices for metals (`occopt`, `tsmear`, k-grid density).
- Geometry/typing mismatch (`natom`, `typat`, coordinates, pseudo mapping).
- Skipping convergence sweeps on key observables (total energies alone are insufficient for all targets).

### Convergence and validation checks
- Target observables are stable w.r.t. `ecut` and k-mesh refinement.
- SCF and structural stopping criteria are met consistently across restarts.
- Symmetry and Brillouin-zone settings do not introduce unintended artifacts.
- Response calculations reproduce expected trends and are free from obvious numerical pathologies.

## Scope
- Handle variable discovery, model setup, and correctness-critical parameterization.
- Focus on robust, reproducible input construction patterns.

## Primary documentation references
- `doc/topics/_GSintroduction.md`
- `doc/guide/new_user.md`
- `doc/tutorial/base2.md`
- `doc/tutorial/rf1.md`
- `doc/tutorial/paw1.md`
- `doc/tutorial/paral_dfpt.md`
- `doc/faq/dfpt.md`
- `doc/theory/geometry.md`
- `doc/variables/DOC_EFIELD_BEC_DIEL.txt`
- `doc/topics/_PseudosPAW.md`

## Workflow
- Start with docs/tutorials for method-level setup.
- Use `references/doc_map.md` for full topical variable/model inventory.
- Use tests/tutorial inputs as runnable templates where available.
- Escalate to source maps only for unresolved parser/implementation details.
- Cite exact file paths in all recommendations.

## Tutorials and examples
- `doc/tutorial`
- `tests/tutorial/Input`
- `tests/tutoparal/Input`

## Test references
- `tests/fast`
- `tests/v1`
- `tests/tutorespfn`

## Optional deeper inspection
- `abimkdocs`
- `src/57_iovars`
- `src/64_psp`
- `src/41_geometry`

## Source entry points for unresolved issues
- `src/57_iovars/m_invars1.F90`
- `src/57_iovars/m_invars2.F90`
- `src/57_iovars/m_chkinp.F90`
- `src/57_iovars/m_inkpts.F90`
- `src/41_geometry/m_spgdata.F90`
- `src/64_psp/m_pspini.F90`
- `src/64_psp/m_psps.F90`
- `src/64_psp/m_psp1.F90`
- `src/64_psp/m_psp6.F90`
- `abimkdocs/variables_abinit.py`
- `abimkdocs/variables.py`
- Prefer targeted search (for example: `rg -n "<symbol_or_keyword>" src/57_iovars src/64_psp src/41_geometry abimkdocs`).
