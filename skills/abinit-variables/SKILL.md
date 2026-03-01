---
name: abinit-variables
description: Use this skill for ABINIT variable semantics, parser behavior, and variable-driven simulation sanity workflows.
---

# abinit: Variables

## High-Signal Playbook

### Route conditions
- Route to `abinit-inputs-and-modeling` for full physical-model setup decisions.
- Route to `abinit-getting-started` for first-run basics and output anatomy.
- Route to `abinit-api-and-scripting` for programmatic variable extraction.

### Triage questions
- Which variable family is in scope (SCF, k-point, electric field, DFPT, PAW)?
- Is the question about meaning, allowed combinations, or parser behavior?
- Is there a reproducible input snippet showing the issue?
- Which observable should confirm the variable choice is correct?

### Canonical workflow
1. Read the variable docs entry and related topic page.
2. Check parser/validation behavior in iovars source only if docs are ambiguous.
3. Run a small tutorial-style input where the variable is active.
4. Change one variable at a time and compare outputs.
5. Promote settings only after observable-level stability checks.

### Minimal working examples
```sh
# Baseline run for variable sanity checks
export ABI_PSPDIR="$PWD/tests/Pspdir"
abinit tests/tutorial/Input/tbase2_1.abi > var_base.log
```

```sh
# Variable-centric follow-up (different convergence profile)
export ABI_PSPDIR="$PWD/tests/Pspdir"
abinit tests/tutorial/Input/tbase2_2.abi > var_followup.log
```

### Pitfalls and fixes
- Editing many variables simultaneously and losing causal attribution.
- Assuming tutorial defaults are publication-grade.
- Ignoring variable coupling constraints (for example, smearing + k-point density).
- Relying on prose only when parser constraints should be checked in source.

### Validation checkpoints
- Variable change produces expected directional effect on target observable.
- SCF/response criteria remain satisfied after variable adjustments.
- No parser/consistency warnings are emitted.
- Results are stable under small additional tightening.

## Scope
- Handle variable semantics, parser constraints, and variable-driven sanity workflows.
- Keep recommendations tied to reproducible input/output checks.

## Primary documentation references
- `doc/variables/DOC_EFIELD_BEC_DIEL.txt`
- `doc/topics/_GSintroduction.md`
- `doc/topics/_PseudosPAW.md`
- `doc/guide/new_user.md`
- `doc/tutorial/base2.md`

## Workflow
- Start from docs, then run a minimal reproducible input.
- Use `references/doc_map.md` for expanded variable-related docs.
- Escalate to `references/source_map.md` for parser/function-level behavior checks.
- Cite exact variable names, paths, and commands.

## Tutorials and examples
- `tests/tutorial/Input/tbase2_1.abi`
- `tests/tutorial/Input/tbase2_2.abi`
- `tests/tutorespfn/Input/trf1_1.abi`

## Test references
- `tests/tutorial`
- `tests/tutorespfn`
- `tests/runtests.py`

## Optional deeper inspection
- `abimkdocs`
- `src/57_iovars`
- `src/44_abitypes_defs`
- `src/65_paw`

## Source entry points for unresolved issues
- `abimkdocs/variables_abinit.py`
- `abimkdocs/variables.py`
- `src/57_iovars/m_invars1.F90`
- `src/57_iovars/m_invars2.F90`
- `src/57_iovars/m_chkinp.F90`
- `src/44_abitypes_defs/m_efield.F90`
- `src/65_paw/m_paw_efield.F90`
- Prefer targeted search (for example: `rg -n "<symbol_or_keyword>" abimkdocs src/57_iovars src/44_abitypes_defs src/65_paw src/77_ddb`).
