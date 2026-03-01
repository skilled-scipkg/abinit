# abinit source map: API and Scripting

Generated from source roots:
- `abimkdocs`
- `bindings`
- `scripts`
- `shared`
- `src`
- `tests/pymods`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<api|yaml|cut3d|psp8|invocation>" src/67_python_invocation_ext src/95_drive src/98_main shared/common/src/17_yaml_out bindings tests/pymods scripts`
- `rg -n "subroutine|function|module|class|def" src/67_python_invocation_ext src/95_drive src/98_main shared/common/src/17_yaml_out bindings tests/pymods scripts`

## Suggested source entry points (function-level)
- `src/98_main/cut3d.F90` | CLI entry for `cut3d` behavior.
- `src/95_drive/m_cut3d.F90` | `cut3d` driver/control flow.
- `src/67_python_invocation_ext/m_invocation_tools.F90` | Python invocation/tool bridge points.
- `src/64_psp/m_psp8.F90` | PSP8 parser behavior.
- `shared/common/src/17_yaml_out/m_yaml.F90` | YAML serialization core.
- `shared/common/src/17_yaml_out/m_pair_list.F90` | YAML key-value/pair handling.
- `tests/pymods/yaml_tools/tester.py` | Python YAML test runner API surface.
- `tests/pymods/yaml_tools/conf_parser.py` | YAML test config parser behavior.
- `bindings/configure.ac` | bindings configure-time feature checks.
- `bindings/config/makefiles/libpaw.am` | libpaw bindings build wiring.
- `shared/libpaw/config/abinit/automake/library.py` | libpaw automake/python glue.
