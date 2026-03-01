---
name: abinit-simulation-workflows
description: Use this skill for end-to-end ABINIT run patterns (single-point, chained DFPT/restart, post-processing interfaces) with practical validation checkpoints.
---

# abinit: Simulation Workflows

## High-Signal Playbook

### Route conditions
- Route to `abinit-getting-started` for first-run orientation.
- Route to `abinit-inputs-and-modeling` for variable/method correctness.
- Route to `abinit-parallel-hpc` for scaling/launcher specifics.
- Route to `abinit-api-and-scripting` for heavy automation and external toolchains.

### Triage questions
- Is the workflow single-step, multi-step chained, or restart-based?
- Which files must be handed off between steps (`WFK`, `WFQ`, `DEN`, DDB artifacts)?
- Are external postprocessors/interfaces required (Wannier90, Z2Pack, cut3d)?
- What is the primary validation observable for workflow success?

### Canonical workflow
1. Run a baseline GS input to validate environment.
2. Execute the next step(s) with explicit handoff files.
3. Keep each step log and check completion markers.
4. Validate intermediate artifacts before launching the next stage.
5. Only then adapt to production-size systems.

### Minimal working examples
```sh
# Baseline GS run
export ABI_PSPDIR="$PWD/tests/Pspdir"
abinit tests/tutorial/Input/tbase2_1.abi > tbase2_1.log
```

```sh
# Two-step DFPT chain
export ABI_PSPDIR="$PWD/tests/Pspdir"
mpirun -n 4 abinit tests/tutoparal/Input/tdfpt_01.abi > tdfpt_01.log
cp tdfpt_01.o_WFK tdfpt_02.i_WFK
cp tdfpt_01.o_WFK tdfpt_02.i_WFQ
mpirun -n 4 abinit tests/tutoparal/Input/tdfpt_02.abi > tdfpt_02.log
```

```sh
# Optional plugin workflow entrypoint
abinit tests/tutoplugs/Input/tw90_1.abi > tw90_1.log
```

### Pitfalls and fixes
- Skipping intermediate-file validation between chained steps.
- Reusing stale restart files after changing physical settings.
- Assuming plugin workflows are available without dependency checks.
- Focusing only on final outputs while missing warnings in intermediate logs.

### Validation checkpoints
- Every step log ends cleanly with no fatal errors.
- Required handoff files exist before the next command.
- Restart/chained runs reproduce expected continuation behavior.
- Target observables remain stable under small reruns.

## Scope
- Handle practical orchestration of ABINIT simulation chains and restarts.
- Focus on robust execution flow and checkpoint validation.

## Primary documentation references
- `doc/faq/ground_state.md`
- `doc/guide/cut3d.md`
- `doc/tutorial/wannier90.md`
- `doc/tutorial/z2pack.md`
- `tests/tutoparal/README_dfpt.txt`
- `tests/tutoplugs/Input/tw90_1.abi`

## Workflow
- Start from docs/tutorial sequence for the requested workflow style.
- Use `references/doc_map.md` for full workflow-oriented inventory.
- Run stepwise and validate handoff artifacts before continuing.
- Escalate to `references/source_map.md` for function-level behavior checks.
- Cite exact paths for inputs, intermediate files, and logs.

## Tutorials and examples
- `tests/tutorial/Input/tbase2_1.abi`
- `tests/tutoparal/Input/tdfpt_01.abi`
- `tests/tutoparal/Input/tdfpt_02.abi`
- `tests/tutoplugs/Input/tw90_1.abi`
- `tests/tutoplugs/Input/tz2_2.abi`

## Test references
- `tests/tutorial`
- `tests/tutoparal`
- `tests/tutoplugs`

## Optional deeper inspection
- `src/95_drive`
- `src/98_main`
- `src/71_wannier`
- `shared/common/src/18_timing`

## Source entry points for unresolved issues
- `src/98_main/abinit.F90`
- `src/95_drive/m_driver.F90`
- `src/95_drive/m_gstate.F90`
- `src/95_drive/m_dfpt_looppert.F90`
- `src/95_drive/m_cut3d.F90`
- `src/71_wannier/defs_wannier90.F90`
- Prefer targeted search (for example: `rg -n "<symbol_or_keyword>" src/95_drive src/98_main src/71_wannier shared/common/src/18_timing`).
