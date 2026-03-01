# abinit source map: Analysis and Output

Generated from source roots:
- `scripts`
- `shared`
- `src`
- `tests/pymods`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `rg -n "<observable|output_format|file_ext>" src/56_io_mpi src/57_iovars shared/common/src/17_yaml_out scripts/post_processing tests/pymods`
- `rg -n "subroutine|function|module|class|def" src/56_io_mpi src/57_iovars shared/common/src/17_yaml_out scripts/post_processing tests/pymods`

## Suggested source entry points (function-level)
- `src/57_iovars/m_outvars.F90` | output-variable registration and output block controls.
- `src/56_io_mpi/m_hdr.F90` | header I/O for ABINIT binary/text artifacts.
- `src/56_io_mpi/m_rwwf.F90` | wavefunction read/write behavior.
- `src/56_io_mpi/m_abi_etsf.F90` | ETSF/NetCDF I/O interface points.
- `shared/common/src/17_yaml_out/m_yaml.F90` | YAML emission paths used in tests and logs.
- `scripts/post_processing/plot_bandstructure.py` | bandstructure plotting workflow.
- `scripts/post_processing/plot_bs.py` | alternative bandstructure plotting path.
- `scripts/post_processing/appa/utility/analysis.py` | APPA analysis helpers.
- `scripts/post_processing/wannier_bandstructure.py` | Wannier band post-processing.
- `tests/pymods/abo_file_analysis.py` | parser logic for `.abo`-style analysis.
- `tests/pymods/data_extractor.py` | extracted-data utilities for result checks.
