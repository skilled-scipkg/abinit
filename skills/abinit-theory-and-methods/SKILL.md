---
name: abinit-theory-and-methods
description: Use this skill for theory-to-implementation mapping (BSE, pseudopotentials, noncollinear, MBPT-related methods) with runnable sanity paths.
---

# abinit: Theory and Methods

## High-Signal Playbook

### Route conditions
- Route to `abinit-examples-and-tutorials` for step-by-step method walkthroughs.
- Route to `abinit-inputs-and-modeling` for concrete variable selection and convergence tuning.
- Route to `abinit-analysis-and-output` for post-processing interpretation.

### Triage questions
- Which method family is requested (BSE, GW/MBPT, noncollinear magnetism, pseudopotentials)?
- Is the user asking conceptual derivation or implementation behavior?
- Which observable should validate the method usage?
- Which tutorial/test input is the closest runnable anchor?

### Canonical workflow
1. Start from theory docs for equations and assumptions.
2. Map to a runnable tutorial input for that method family.
3. Run the minimal case and validate expected qualitative behavior.
4. Inspect source entry points for the requested algorithm details.
5. Cross-check assumptions before scaling to production systems.

### Minimal working examples
```sh
# GW tutorial starting point
export ABI_PSPDIR="$PWD/tests/Pspdir"
abinit tests/tutorial/Input/tgw1_1.abi > tgw1_1.log
```

```sh
# MBT-oriented parallel tutorial anchor
export ABI_PSPDIR="$PWD/tests/Pspdir"
mpirun -n 4 abinit tests/tutoparal/Input/tmbt_1.abi > tmbt_1.log
```

### Pitfalls and fixes
- Applying formal equations outside their approximation domain.
- Interpreting unconverged tutorial defaults as final science-grade settings.
- Skipping cross-check between theory assumptions and chosen input variables.
- Confusing implementation modules with user-facing method controls.

### Validation checkpoints
- Tutorial run completes and reproduces expected qualitative trends.
- Core observable behaves consistently under small convergence tightening.
- Theory assumptions match the executed mode and variable set.
- Source-level interpretation points to the same algorithmic path as docs.

## Scope
- Handle formal-method explanations and their implementation entry points.
- Keep advice tied to runnable repository cases whenever possible.

## Primary documentation references
- `doc/theory/bse.md`
- `doc/theory/noncollinear.md`
- `doc/theory/pseudopotentials.md`
- `doc/theory/spherical_harmonics.md`
- `doc/theory/acronyms.md`
- `doc/theory/mbt.md`

## Workflow
- Start from theory docs, then connect to tutorial/test anchors.
- Use `references/doc_map.md` for the complete theory doc inventory.
- Escalate to `references/source_map.md` for function-level algorithm checks.
- Cite exact doc and source paths.

## Tutorials and examples
- `tests/tutorial/Input/tgw1_1.abi`
- `tests/tutorial/Input/tgw2_1.abi`
- `tests/tutoparal/Input/tmbt_1.abi`
- `tests/tutorespfn/Input/trf1_1.abi`

## Test references
- `tests/tutorial/Refs/tgw1_1.abo`
- `tests/tutoparal/Refs/tmbt_1_MPI64.abo`

## Optional deeper inspection
- `src/71_bse`
- `src/78_effpot`
- `src/64_psp`
- `shared/common/src/28_numeric_noabirule`

## Source entry points for unresolved issues
- `src/71_bse/m_hexc.F90`
- `src/71_bse/m_exc_build.F90`
- `src/71_bse/m_exc_diago.F90`
- `src/71_bse/m_exc_spectra.F90`
- `src/71_bse/m_haydock.F90`
- `src/78_effpot/m_harmonics_terms.F90`
- `src/64_psp/m_psp8.F90`
- Prefer targeted search (for example: `rg -n "<symbol_or_keyword>" src/71_bse src/78_effpot src/64_psp src/67_common shared/common/src/28_numeric_noabirule`).
