# Contributing

## Tracked files

Only patcher files and the vanilla sources they read are tracked. Those sources are the minimal set of original files picked from vanilla data to satisfy the build, and they all live in `common/`. The full extracted vanilla data stays in the git-ignored `ref/`, generated packs in the git-ignored `build/`.

## How to develop a datapack

1. extract the old and new version data into `ref/`.
2. compare the data between versions with your usual diff tools, especially biome data, noise settings and density functions. `tools/json_diff.py` is a minimal helper that only reports differing paths, so keep using your usual tools alongside it.
3. for minor changes, create `x_patch/` in `common/` and add the changed vanilla data files, then write patcher files.
4. for major changes, create `x_y_z/` in `common/` and add the group of changed vanilla data files, then write patcher files.
5. deliver each version as a sub-pack override of the shared base no matter how much it changes; the `common/` files above are only the vanilla sources the patchers read.
6. test before release. `python build.py` only produces the builds, it does not test them; test the environment yourself, for example a server and a client of the target MC version.

## Patcher files

A patcher is a Python module placed anywhere in a version directory; its interface is documented in the [framework README](tools/README.md).
