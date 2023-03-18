# cmake-vcpkg-imgui-emscripten

**IF ANYONE FOUND THIS HERE, I HAVE A QUESTION:**
- **[HOW CAN MULTI-THREADING BE ACTIVATED IN EMSCRIPTEN?](https://github.com/aarlt/cmake_vcpkg_imgui_emscripten/issues/1#issue-1630469401)**

## Normal Build

```shell
git clone https://github.com/aarlt/cmake-vcpkg-imgui-emscripten
cd cmake-vcpkg-imgui-emscripten
mkdir build
cd build
cmake ..
make
```

## Emscripten Build

- install `emsdk`

```shell
git clone https://github.com/aarlt/cmake-vcpkg-imgui-emscripten
cd cmake-vcpkg-imgui-emscripten
mkdir build
cd build
emcmake cmake .. "-DVCPKG_CHAINLOAD_TOOLCHAIN_FILE=${EMSDK}/upstream/emscripten/cmake/Modules/Platform/Emscripten.cmake" "-DVCPKG_TARGET_TRIPLET=wasm32-emscripten" "-DCMAKE_TOOLCHAIN_FILE=${VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake"
make
```

### Start http-server

```shell
npx http-server
```
