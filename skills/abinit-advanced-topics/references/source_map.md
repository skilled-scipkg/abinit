# abinit source map: Advanced Topics

Generated from source roots:
- `abimkdocs`
- `abimkdocs_plugin`
- `scripts`
- `cmake`
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" scripts cmake src abimkdocs abimkdocs_plugin`
- `rg -n "subroutine|function|module|class|def" scripts src abimkdocs abimkdocs_plugin`

## Suggested source entry points (function-level)
- `scripts/post_processing/appa/gui/about.py` | APPA about-dialog text and metadata wiring.
- `src/41_geometry/m_spgdata.F90` | space-group table/module logic used by symmetry paths.
- `src/98_main/abinit.F90` | startup banner/version/license-adjacent runtime messaging.
- `cmake/abinit_install.cmake` | install-time packaging/install rule behavior.
- `abimkdocs/variables.py` | docs-variable index generation hooks referenced by topic pages.
