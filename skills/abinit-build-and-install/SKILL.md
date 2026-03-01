---
name: abinit-build-and-install
description: Use this skill for ABINIT compilation, dependency setup, toolchain choices (Autotools/CMake), and post-build smoke validation.
---

# abinit: Build and Install

## High-Signal Playbook

### Route conditions
- Route to `abinit-troubleshooting` when the user has runtime crashes, numerics, or platform-specific failures after a successful build.
- Route to `abinit-parallel-hpc` for MPI/OpenMP/GPU scaling, launcher syntax, or scheduler integration.
- Route to `abinit-inputs-and-modeling` for input-variable semantics and physical model setup.

### Triage questions
- Which build path is required: `Autotools` or `CMake`?
- Which compiler stack is used (`gfortran`, `ifort/ifx`, `nvhpc`) and versions?
- Which dependencies are mandatory on this host (`BLAS/LAPACK`, `NetCDF4`, `HDF5`, `LibXC`, optional `MPI`, optional `Wannier90`)?
- Is this a clean out-of-tree build directory?
- Which phase fails: configure/cmake detect, compile, link, or tests?
- Is this a user install (`--prefix`) or system install?

### Canonical workflow
1. Choose build system from `doc/installation.md` (`Autotools` default, `CMake` experimental but supported).
2. Verify toolchain and dependency discovery (`which gfortran gcc make cmake pkg-config`).
3. Build out-of-tree.
4. Configure using one path:
   - `Autotools`: `../configure` (or `../configure FC=gfortran ...`).
   - `CMake`: `cmake -S ..` with optional `PKG_CONFIG_PATH` and compiler env vars.
5. Compile with `make -jN`.
6. Run smoke validation (`make check`, then optionally `make test_fast`).
7. Run focused test subset when needed: `cd tests && ./runtests.py --keywords MINIMAL --yaml-simplified-diff`.
8. Install (`make install`) only after smoke tests pass.

### Minimal working example
```sh
# Autotools (docs-first path)
mkdir -p build-autotools && cd build-autotools
../configure FC=gfortran
make -j4
make check
```

```sh
# CMake path with explicit pkg-config hints
mkdir -p _build_cmake && cd _build_cmake
PKG_CONFIG_PATH="/path/to/netcdf/pkgconfig:/path/to/libxc/pkgconfig:$PKG_CONFIG_PATH" \
  cmake -S ..
make -j8
make check
```

### Pitfalls and fixes
- Missing external libs at configure time: follow dependency list in `doc/installation.md` and pass explicit paths (`PKG_CONFIG_PATH`/`CMAKE_PREFIX_PATH`).
- In-source build contamination: rebuild in a fresh directory; see `cmake/prevent_build_in_source.cmake`.
- `hostname.ac9` confusion: use precedence rules in `doc/installation.md` (`build dir` > `source dir` > `~/.abinit/build`).
- Assuming test pseudos are production-grade: `tests/Pspdir` is for tests, not production (`doc/guide/new_user.md`).
- Platform/compiler exclusions: consult `KNOWN_PROBLEMS` before attributing failures to local changes.
- Mixing stale objects across options: clean or recreate build dir when toggling compiler/feature flags.

### Convergence and validation checks
- The built `abinit` executable is runnable (`abinit -b` for build info).
- `make check` passes (equivalent minimal subset is documented in `doc/installation.md`).
- `make test_fast` reports clean completion for built-in sanity.
- A small tutorial input runs to completion and writes expected `.abo`/log outputs.

## Scope
- Handle build, installation, compilation, dependency configuration, and quick post-build validation.
- Keep guidance docs-first; escalate to source only when behavior/details are unresolved.

## Primary documentation references
- `README.md`
- `INSTALL.md`
- `INSTALL`
- `doc/installation.md`
- `doc/tutorial/abinit_build.md`
- `doc/faq/configuration_and_compilation.md`
- `doc/help_make/help_make_top.txt`
- `doc/help_make/help_make_core.txt`
- `doc/help_make/help_make_doc.txt`
- `KNOWN_PROBLEMS`

## Workflow
- Start from `doc/installation.md` for install/build decision points.
- Use `references/doc_map.md` for complete build/install doc inventory.
- Validate with `make check` / `tests/runtests.py` before source-level debugging.
- Escalate to `references/source_map.md` only when documentation is insufficient.
- Cite exact file paths when answering build or diagnostics questions.

## Tutorials and examples
- `doc/tutorial/abinit_build.md`
- `doc/tutorial/lattice_model.md`
- `doc/tutorial/lwf_model.md`
- `doc/tutorial/spin_model.md`

## Test references
- `tests/README.md`
- `tests/runtests.py`

## Optional deeper inspection
- `cmake`
- `config`
- `shared`
- `src`

## Source entry points for unresolved issues
- `configure.ac`
- `CMakeLists.txt`
- `cmake/options.cmake`
- `cmake/abinit_install.cmake`
- `cmake/prevent_build_in_source.cmake`
- `cmake/build_or_find_kokkos.cmake`
- `cmake/build_or_find_yakl.cmake`
- `shared/common/src/14_hidewrite/generate_build_info.cmake`
- `shared/common/src/14_hidewrite/m_build_info.F90.cmake.in`
- `src/98_main/CMakeLists.txt`
- `tests/runtests.py`
- Prefer targeted search (for example: `rg -n "<symbol_or_keyword>" cmake config shared src tests`).
