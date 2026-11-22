# VibeGeode Jukebox fork

- Upstream: https://github.com/Fleeym/jukebox
- Upstream source commit: `abb0b3c9f87336acb594278de5b25525d9177dcf`
- License: MIT; retain the upstream `LICENSE` and copyright.
- Target: Windows x64, Geometry Dash 2.2091, Geode 6.0.0-beta.1.
- SDK: Geode `0bf4857770207b0f6df47ac8d5e615f013d757e9`.
- Bindings: `78d5bb4eb0732dd636ae16d4dcf6e5ce84ec1221`, confirmed from the installed beta.1 loader log.
- Mod ID remains `fleym.nongd` to retain its existing Geode storage and songs.
- Local beta build version: `3.8.0-beta.1` (Geode's parser accepts its `beta` tag).

Build with the matching SDK and bindings rather than the workspace default/nightly SDK:

```bash
source /home/dragon/Repositories/geode/env.sh
export GEODE_SDK=/home/dragon/Repositories/VibeGeode/sdk/geode-v6.0.0-beta.1
export GEODE_BINDINGS_REPO_PATH=/home/dragon/Repositories/VibeGeode/sdk/bindings-beta1
cmake -S . -B build-win -G Ninja \
  -DCMAKE_TOOLCHAIN_FILE="$CMAKE_TOOLCHAIN_FILE" \
  -DSPLAT_DIR="$SPLAT_DIR" -DHOST_ARCH=x86_64 \
  -DCMAKE_BUILD_TYPE=RelWithDebInfo -DGEODE_DONT_INSTALL_MODS=ON
cmake --build build-win
python /home/dragon/Repositories/geode/tools/verify-package.py build-win/fleym.nongd.geode
```

`build-win` produces a Windows x64 package only. The package must be copied to
the dedicated Windows test VM after backing up the currently installed package
and Jukebox's existing Geode data. Verify a fresh launch log before requesting
manual testing. Do not restore VM snapshots or stop an existing game without
authorization.
