# Game of Life

C++ implementation of game of life.

## PREREQUISITES

Following packages are required to build the project:

* Git >= 2.48
* Ninja >= 1.12
* Clang >= 19.1 / GCC >= 14.2

## SETUP

Either use one of the packages in [Releases](https://github.com/briansalehi/life/releases), or build the project manually:

```sh
git clone https://github.com/briansalehi/life.git
cmake -G Ninja -S life -B life-release -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=$HOME/.local
cmake --build life-release --config release --parallel
cmake --install life-release
```

## Use

Include this library into your project and link it to your program:

```cmake
include(FetchContent)

FetchContent_Declare(life GIT_REPOSITORY https://github.com/briansalehi/life.git GIT_TAG main)
FetchContent_MakeAvailable(life)

target_link_libraries(<target> PRIVATE life)
```

## LICENSE

This repository is licensed under [GPL-3.0](LICENSE.md).

## CONTRIBUTION

Please feel free to suggest better implementations of game of life in the most recent C++ standard.
