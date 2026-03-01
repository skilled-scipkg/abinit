# abinit source map: Build and Install

Generated from source roots:
- `cmake`
- `config`
- `shared`
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<dependency|compiler|option|install|pkgconfig>" configure.ac CMakeLists.txt cmake config shared/common/src/14_hidewrite src/98_main`
- `rg -n "function\(|macro\(|option\(|subroutine|module" CMakeLists.txt cmake configure.ac shared/common/src/14_hidewrite src/98_main/CMakeLists.txt`

## Suggested source entry points (function-level)
- `configure.ac` | Autotools feature detection and dependency checks.
- `CMakeLists.txt` | top-level CMake target/options orchestration.
- `cmake/options.cmake` | configurable ABINIT feature toggles.
- `cmake/abinit_install.cmake` | install target logic.
- `cmake/prevent_build_in_source.cmake` | in-source build guard behavior.
- `cmake/build_or_find_kokkos.cmake` | Kokkos dependency resolution.
- `cmake/build_or_find_yakl.cmake` | YAKL dependency resolution.
- `config/scripts/makemake` | generated build-system bootstrap helper.
- `shared/common/src/14_hidewrite/generate_build_info.cmake` | build metadata generation.
- `shared/common/src/14_hidewrite/m_build_info.F90.cmake.in` | compiled build-info module template.
- `src/98_main/CMakeLists.txt` | main executable target linkage.
