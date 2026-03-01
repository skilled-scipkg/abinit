---
name: abinit-analysis-and-output
description: Use this skill for ABINIT output interpretation, output-file sanity checks, and post-processing handoff with scripts/tools.
---

# abinit: Analysis and Output

## High-Signal Playbook

### Route conditions
- Route to `abinit-inputs-and-modeling` when incorrect physics setup is the primary issue.
- Route to `abinit-api-and-scripting` for parser automation and external scripting APIs.
- Route to `abinit-troubleshooting` for hard runtime failures.

### Triage questions
- Which output artifact is under inspection (`.abo`, NetCDF, DDB-derived files, plots)?
- Is the goal quick sanity, convergence analysis, or publication-quality post-processing?
- Is the issue missing output, inconsistent values, or parser/plot failure?
- Are reference outputs available for comparison?

### Canonical workflow
1. Run a known tutorial/test case to produce baseline outputs.
2. Inspect logs and `.abo` summary blocks first.
3. Parse/post-process with one tool at a time.
4. Compare against tutorial or reference output trends.
5. Escalate to source only if output generation/parsing remains unclear.

### Minimal working examples
```sh
export ABI_PSPDIR="$PWD/tests/Pspdir"
abinit tests/tutorial/Input/tbase4_1.abi > tbase4_1.log
```

```sh
# Quick output sanity scan
grep -niE "warning|error|etotal|nstep|timing" tbase4_1.log
python scripts/post_processing/plot_bs.py --help
```

### Pitfalls and fixes
- Reading only final numbers without checking convergence/warning sections.
- Mixing files from different runs in post-processing scripts.
- Using parser assumptions from one format on another.
- Skipping comparison to known references before interpreting anomalies.

### Validation checkpoints
- Run completed and produced expected output files.
- Key observables are internally consistent across log/output sections.
- Post-processing scripts load input data without format errors.
- Repeated baseline run gives reproducible values within tolerance.

## Scope
- Handle interpretation and practical analysis of ABINIT outputs.
- Keep workflows runnable from repository-contained examples.

## Primary documentation references
- `doc/guide/cut3d.md`
- `doc/tutorial/optic.md`
- `doc/tutorial/base4.md`
- `doc/developers/codestats.md`
- `doc/maintainers/analysis_targz_size.txt`

## Workflow
- Start with docs and one reproducible tutorial run.
- Use `references/doc_map.md` for the topic's full document list.
- Use `tests` and `scripts/post_processing` for behavior references.
- Escalate to `references/source_map.md` for function-level checks.
- Cite exact paths for outputs and post-processing commands.

## Tutorials and examples
- `tests/tutorial/Input/tbase4_1.abi`
- `tests/tutorial/Input/tbase4_2.abi`
- `scripts/post_processing/plot_bandstructure.py`
- `scripts/post_processing/plot_bs.py`

## Test references
- `tests/pymods/abo_file_analysis.py`
- `tests/pymods/data_extractor.py`
- `tests/runtests.py`

## Optional deeper inspection
- `scripts/post_processing`
- `src/56_io_mpi`
- `src/57_iovars`
- `shared/common/src/17_yaml_out`

## Source entry points for unresolved issues
- `src/57_iovars/m_outvars.F90`
- `src/56_io_mpi/m_hdr.F90`
- `src/56_io_mpi/m_rwwf.F90`
- `src/56_io_mpi/m_abi_etsf.F90`
- `shared/common/src/17_yaml_out/m_yaml.F90`
- `scripts/post_processing/appa/utility/analysis.py`
- Prefer targeted search (for example: `rg -n "<symbol_or_keyword>" src/56_io_mpi src/57_iovars shared/common/src/17_yaml_out scripts/post_processing tests/pymods`).
