---
name: abinit-getting-started
description: Use this skill for first ABINIT runs, first input/output anatomy, and early-stage workflow handoff to deeper topic skills.
---

# abinit: Getting Started

## High-Signal Playbook

### Route conditions
- Route to `abinit-build-and-install` if the binary is missing or compilation is incomplete.
- Route to `abinit-inputs-and-modeling` for variable semantics, model choices, and convergence strategy.
- Route to `abinit-examples-and-tutorials` for method-specific walkthroughs.
- Route to `abinit-parallel-hpc` for cluster launcher and scalability questions.

### Triage questions
- Is `abinit` already built and runnable from this environment?
- Is this a first ground-state run, geometry relaxation, or response-function run?
- Is the target system molecular or periodic?
- Which pseudopotential family is being used (test vs production)?
- Which outputs matter first (`.abo`, `DEN`, `WFK`, forces, stress)?
- Which stage fails (input parsing, SCF convergence, output interpretation)?

### Canonical workflow
1. Confirm installation and binary availability.
2. Start from a known minimal tutorial input (`tests/tutorial/Input/tbase2_1.abi` or the minimal GS skeleton in `doc/topics/_GSintroduction.md`).
3. Set pseudopotential path and run a single-job smoke test.
4. Read both run log and `.abo` output; check for warnings/errors.
5. Identify key variables (`ecut`, `ngkpt`, `nstep`, `tolvrs`/`toldfe`) and tighten from tutorial defaults.
6. Repeat with small convergence sweeps before moving to production settings.
7. Hand off to modeling/examples skills for method-specific workflows.

### Minimal working example
```sh
# Quick smoke run with tutorial input
export ABI_PSPDIR="$PWD/tests/Pspdir"
abinit tests/tutorial/Input/tbase2_1.abi > tbase2_1.log
```

```abinit
# Minimal ground-state skeleton (from doc/topics/_GSintroduction.md style)
acell 3*7.60
rprim 0.0 0.5 0.5
      0.5 0.0 0.5
      0.5 0.5 0.0
ntypat 1
znucl 13
natom 1
typat 1
xred 0.0 0.0 0.0
ecut 6.0
ngkpt 2 2 2
nstep 10
toldfe 1.0d-6
```

### Pitfalls and fixes
- Treating tutorial thresholds as production defaults: increase `ecut`, k-mesh density, and tighten SCF tolerances.
- Using `tests/Pspdir` pseudopotentials for production: use recommended ABINIT atomic-data tables (`doc/guide/new_user.md`).
- Checking only `.abo` or only stdout: inspect both output and log files.
- Mixing dataset-specific and global vars incorrectly (`ndtset`/suffix patterns): follow tutorial examples carefully.
- Ignoring warnings about pseudopotential/atom-type mismatch (`znucl`, `typat`, pseudo file selection).

### Convergence and validation checks
- SCF reaches stopping criterion before `nstep`.
- Total energy is stable under `ecut` and `ngkpt` increases.
- Relaxation runs satisfy force criterion (`tolmxf`) when geometry optimization is requested.
- Restart from density/wavefunction files reproduces expected continuation behavior.

## Scope
- Handle first-run setup, input-output anatomy, and beginner-safe run patterns.
- Keep responses practical and docs-first; avoid deep method internals unless requested.

## Primary documentation references
- `README.md`
- `doc/index.md`
- `doc/guide/new_user.md`
- `doc/installation.md`
- `doc/tutorial/index.md`
- `doc/topics/_GSintroduction.md`
- `doc/tutorial/base2.md`
- `tests/tutorial/Input/tbase2_1.abi`

## Workflow
- Start with beginner docs and one runnable tutorial input.
- Use `references/doc_map.md` for broader beginner/tutorial pages.
- Use tutorial/test inputs as known-good templates before custom inputs.
- Escalate to `references/source_map.md` only for unresolved behavior details.
- Cite exact file paths in answers.

## Tutorials and examples
- `doc/tutorial/index.md`
- `doc/tutorial/base2.md`
- `doc/tutorial/base4.md`
- `tests/tutorial/Input`

## Test references
- `tests/tutorial`
- `tests/fast`

## Optional deeper inspection
- `abimkdocs`
- `scripts`
- `src`

## Source entry points for unresolved issues
- `src/98_main/abinit.F90`
- `src/95_drive/m_driver.F90`
- `src/95_drive/m_gstate.F90`
- `src/57_iovars/m_invars1.F90`
- `src/57_iovars/m_invars2.F90`
- `src/57_iovars/m_chkinp.F90`
- `src/57_iovars/m_outvars.F90`
- `src/64_psp/m_pspini.F90`
- `src/64_psp/m_psps.F90`
- `src/64_psp/m_psp1.F90`
- Prefer targeted search (for example: `rg -n "<symbol_or_keyword>" src/57_iovars src/64_psp src/95_drive src/98_main`).
