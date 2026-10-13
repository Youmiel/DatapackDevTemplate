# Contributing

Contributions are welcome. The build system is a small Python program with a single third-party dependency (`chardet`), so any Python 3 runtime can run it. Run the scripts from the project root:

```
python build.py     # build and pack every version
python clean.py     # remove __pycache__ folders
```

## Tracked files

Only patcher files and the vanilla sources they read are tracked. Those sources are the minimal set of original files picked from vanilla data to satisfy the build, and they all live in `common/`. The full extracted vanilla data stays in the git-ignored `ref/`, generated packs in the git-ignored `build/`.

## How to update a datapack

1. extract new and old version worldgen data into `ref/`.
2. compare worldgen data between versions with your usual diff tools, especially biome data, noise settings and density functions. `json_diff.py` is a minimal helper that only reports differing paths, so keep using your usual diff tools alongside it.
3. for minor changes, create `x_patch/` in `common/` and add the changed vanilla data files, then write patcher files.
4. for major changes, create `x_y_z/` in `common/` and add the group of changed vanilla data files (for example biomes and noise settings), then write patcher files.
5. deliver new versions through a sub-pack override no matter how much they change, because that is what the datapack overlay format requires; the `common/` files above are only the vanilla sources read by the patchers.
6. test before release. `python build.py` only produces the builds, it does not test them; build the test environment yourself, for example a server and a client of the target MC version.

## Patcher files

A patcher is a Python module placed anywhere in a version directory. `TYPE`, `reference_file` and `process_single` / `process_multi` form its interface, documented in `script_modules/template/json_patcher.py`.

- the file name is the target file name, with `.` written as `___`, for example `pack___mcmeta.py` generates `pack.mcmeta`.
- a reference may only read the build output of an older version (`MC_*` constants in `build_settings.py`), static files of the current version (`MC_0`) or `common/` (`COMMON`). Versions are built in the order they are declared in `build_settings.py`.
