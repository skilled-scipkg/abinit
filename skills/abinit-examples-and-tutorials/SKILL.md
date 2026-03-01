---
name: abinit-examples-and-tutorials
description: Use this skill for ABINIT tutorial-to-production translation, runnable example selection, and method-specific learning paths.
---

# abinit: Examples and Tutorials

## High-Signal Playbook

### Route conditions
- Route to `abinit-getting-started` for first-run orientation and package basics.
- Route to `abinit-inputs-and-modeling` for detailed variable/model interpretation.
- Route to `abinit-build-and-install` when failures are compilation/environment related.
- Route to `abinit-api-and-scripting` for automation beyond manual tutorial runs.

### Triage questions
- Which method family is requested (basic GS, DFPT, optics, DFT+U, e-ph, positron, etc.)?
- Is the goal reproduction of tutorial numbers or adaptation to a new material?
- Which test/tutorial input can serve as a runnable baseline?
- Is run mode sequential or MPI-parallel?
- Which output quantity must match (energy, phonons, dielectric response, U/J, ...)?
- Are tutorial defaults being reused without convergence tightening?

### Canonical workflow
1. Select the closest tutorial page from `doc/tutorial/index.md`.
2. Locate the matching runnable input under `tests/tutorial/Input` or `tests/tutoparal/Input`.
3. Run tutorial input unchanged once to verify environment.
4. Compare key outputs against tutorial narrative/reference outputs.
5. Tighten convergence parameters for the target system.
6. Adapt geometry/pseudopotentials/k-point settings incrementally.
7. Escalate to source modules only when behavior diverges from docs.

### Minimal working example
```sh
# Basic tutorial reproduction
export ABI_PSPDIR="$PWD/tests/Pspdir"
abinit tests/tutorial/Input/tbase2_1.abi > tbase2_1.log
```

```sh
# Two-step DFPT chain from tests/tutoparal/README_dfpt.txt pattern
mpirun -n 4 abinit tests/tutoparal/Input/tdfpt_01.abi > tdfpt_01.log
cp tdfpt_01.o_WFK tdfpt_02.i_WFK
cp tdfpt_01.o_WFK tdfpt_02.i_WFQ
mpirun -n 4 abinit tests/tutoparal/Input/tdfpt_02.abi > tdfpt_02.log
```

### Pitfalls and fixes
- Assuming tutorial files are production-converged: increase basis/k-point/tolerance settings.
- Skipping chain file transfers in multi-step tutorials (e.g., WFK/WFQ handoff).
- Using test pseudopotentials for production studies.
- Ignoring method prerequisites/dependencies listed in `doc/tutorial/index.md`.
- Comparing only final values without checking warnings/convergence sections.

### Convergence and validation checks
- Tutorial run completes cleanly and key reported quantities are reproduced within expected tolerance.
- Target observable is stable under convergence sweeps.
- Multi-step workflows produce consistent restart handoffs.
- Adapted system retains method assumptions documented in tutorial page.

## Scope
- Handle tutorial selection, reproducible execution, and safe adaptation patterns.
- Keep focus on practical examples tied to documentation and tests.

## Primary documentation references
- `doc/tutorial/index.md`
- `doc/tutorial/base2.md`
- `doc/tutorial/base4.md`
- `doc/tutorial/optic.md`
- `doc/tutorial/dftu.md`
- `doc/tutorial/lruj.md`
- `doc/tutorial/eph4mob.md`
- `doc/tutorial/positron.md`
- `tests/tutorial/Input/tbase2_1.abi`
- `tests/tutoparal/README_dfpt.txt`
- `tests/tutoparal/Input/tdfpt_01.abi`

## Workflow
- Start with docs page, then run corresponding test/tutorial input.
- Use `references/doc_map.md` for complete tutorial inventory.
- Promote examples to production only after convergence revalidation.
- Escalate to `references/source_map.md` for implementation-level clarifications.
- Cite exact tutorial/input paths.

## Tutorials and examples
- `doc/tutorial`
- `tests/tutorial/Input`
- `tests/tutoparal/Input`
- `tests/tutorespfn/Input`

## Test references
- `tests/tutorial`
- `tests/tutoparal`
- `tests/tutorespfn`

## Optional deeper inspection
- `abimkdocs`
- `scripts/post_processing`
- `src`

## Source entry points for unresolved issues
- `abimkdocs/variables_optic.py`
- `src/98_main/optic.F90`
- `src/98_main/lruj.F90`
- `src/69_wfdesc/m_wfd_optic.F90`
- `src/68_dmft/m_dftu_self.F90`
- `src/67_common/m_optic_tools.F90`
- `src/67_common/m_positron.F90`
- `src/67_common/m_nucprop.F90`
- `scripts/post_processing/ab2epw_quad.py`
- Prefer targeted search (for example: `rg -n "<symbol_or_keyword>" src/98_main src/67_common src/68_dmft scripts/post_processing abimkdocs`).
