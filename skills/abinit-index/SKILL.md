---
name: abinit-index
description: Router skill for ABINIT. Classify the request to the right topic skill, stay docs-first, and escalate to source only when needed.
---

# abinit Skills Index

## Route the request
- Classify the request into one topic skill before answering in detail.
- Keep answers docs-first, workflow-level first, source-level only if docs are insufficient.
- Prefer the smallest skill that directly matches user intent.

## Generated topic skills
- `abinit-getting-started`: first calculations, input/output anatomy, onboarding handoff.
- `abinit-build-and-install`: Autotools/CMake setup, dependency wiring, smoke validation.
- `abinit-inputs-and-modeling`: variable interpretation, structure/pseudo setup, convergence-critical modeling.
- `abinit-examples-and-tutorials`: runnable tutorial paths and adaptation patterns.
- `abinit-tests`: regression execution, selection, and TEST_INFO conventions.
- `abinit-developer-guide`: contribution workflow, source-tree/test/doc conventions.
- `abinit-simulation-workflows`: production run/restart/checkpoint patterns.
- `abinit-parallel-hpc`: MPI/OpenMP/GPU execution and scale debugging.
- `abinit-api-and-scripting`: Python/scripts integration and automation.
- `abinit-analysis-and-output`: output formats and post-processing interpretation.
- `abinit-theory-and-methods`: formal method background and algorithm context.
- `abinit-troubleshooting`: known failures and symptom-driven diagnostics.
- `abinit-variables`: variable semantics and parser-behavior entry points.
- `abinit-advanced-topics`: low-frequency single-doc topics (license/legacy/maintainers/spacegroup/todo/external resources).

## Documentation-first roots
- `doc`
- `shared/libpaw/doc`
- `README.md`
- `INSTALL.md`
- `KNOWN_PROBLEMS`

## Tutorials and examples roots
- `doc/tutorial`
- `tests/tutorial`
- `tests/tutoparal`
- `tests/tutorespfn`
- `tests/tutomultibinit`
- `tests/tutoatdep`

## Test roots for behavior checks
- `tests`
- `abimkdocs_tests`

## Escalate only when needed
- Start from the selected skill `Primary documentation references`.
- If insufficient, inspect the selected skill doc map file under its own `references/` directory.
- If still ambiguous, inspect the selected skill source map file under its own `references/` directory.
- Use targeted symbol search during source inspection.

## Source directories for deeper inspection
- `abimkdocs`
- `abimkdocs_plugin`
- `bindings`
- `cmake`
- `config`
- `scripts`
- `shared`
- `src`
