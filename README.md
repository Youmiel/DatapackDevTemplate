# WGDatapackToolkit

> A build framework for Minecraft worldgen datapacks that must support many game versions from one source tree.

A datapack is compiled from small Python patch scripts plus a minimal set of vanilla source files, so generated worldgen JSON is never committed. Each supported MC version is built from its own source directory and may read the build output of an earlier version.

## How it works

- there is one source directory per version, named after that version and listed in `build_settings.py`.
- inside a version directory every `.py` file is a patch, and every other file is a static resource that is copied into the build as-is.
- a patch declares `TYPE`, `reference_file` and `process_single` / `process_multi`. `reference_file` selects the JSON sources to read, `process_single` / `process_multi` return the modified content.
- sources may come from `common/`, from static files of the current version, or from the build output of an already-built older version.
- versions are built in the order they are declared in `build_settings.py`, so references only ever point backwards.

## Layout

- `build_settings.py` — versions, pack names and paths; the only project-specific configuration.
- `build.py` — entry point that builds every configured version and packs it.
- `clean.py` — removes `__pycache__` folders.
- `json_diff.py` — minimal helper that reports differing paths between two JSON files.
- `script_modules/` — the build framework itself; `script_modules/template/json_patcher.py` documents the patch interface.
- `common/` — vanilla source files shared by the patchers.
- `example_pack/` — a minimal buildable example version.

## Using it as a template

1. copy this repository for the new datapack.
2. delete `example_pack/` and the `MC_EXAMPLE` entry in `build_settings.py`.
3. adjust `BUILD_PATH`, `COMMON_PATH`, `EXTRA_FILE` and `PROJECT_VERSION`.
4. add one `MC_*` constant per supported MC version, in build order.
5. write the version source directories and their patchers.

## Requirements

Python 3 and `chardet` (`pip install -r requirements.txt`). See [CONTRIBUTING.md](CONTRIBUTING.md) for the build commands and the datapack maintenance workflow.
