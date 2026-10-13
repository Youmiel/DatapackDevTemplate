# DatapackDevTemplate

> A datapack project template built on the [DatapackDevToolkit](tools/README.md) build framework.

## Layout

- `build_settings.py` — versions, pack names and paths; the only project-specific configuration.
- `build.py` — entry point that feeds `build_settings.py` to the framework in `tools/` and builds every configured version.
- `tools/` — the DatapackDevToolkit build framework, included as a git submodule.
- `common/` — vanilla source files shared by the patchers.
- `example_pack/` — a minimal buildable example version.
- `CONTRIBUTING.md` — datapack maintenance workflow.

## Build

Run from the project root:

```
python build.py                # build and pack every version
python tools/clean.py          # remove __pycache__ folders
python tools/json_diff.py A B  # report differing paths between two JSON files
```

## Using it as a template

1. copy this repository for the new datapack.
2. run `git submodule update --init --recursive` to fetch the framework in `tools/`.
3. delete `example_pack/` and the `MC_EXAMPLE` entry in `build_settings.py`.
4. adjust `BUILD_PATH`, `COMMON_PATH`, `EXTRA_FILE` and `PROJECT_VERSION`.
5. add one `MC_*` constant per supported MC version, in build order.
6. write the version source directories and their patchers.

## Requirements

Python 3 and `chardet` (`pip install -r tools/requirements.txt`). See [CONTRIBUTING.md](CONTRIBUTING.md) for the datapack maintenance workflow and [tools/README.md](tools/README.md) for the framework.
