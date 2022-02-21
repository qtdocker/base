# Qt-docker-base

Repository with multiple docker recipes for C++ projects linked against old standard library and prepared for cross-compilation.

Main feature of this recipes is modern compilers, build systems and 3rd-party libs. You can easily use clang as cross-compiler, described here (https://habr.com/ru/post/599125/). If you don't like clang, gcc is also available (conan prepared only for clang).

I looked here https://github.com/dockcross/dockcross but it uses ancient compilers.
So here you can use:
- Clang-11 - debian-backports for buster, upstream for bullseye.
- Cmake-latest (3.23.0-rc1 - 21.02.2022) - built from sources.
- Other tools are the same as debian:buster repository.
- [Conan](https://conan.io/)-intergrated and prepared for clang-11 and listdc++11.

If you want to compile to arm on amd64 you have 2 ways:
- Cross-compile with cross-compiler and etc. Look at cross-compilation containers
- Compile with qemu as emulator. Look at native containers. But don't forget, you need qemu on a host machine. For example, if you have Debian as host, you need package `qemu-user-static`

### Debian Buster
#### Base arch: armv7a/armhf [![Docker Image CI](https://github.com/qtdocker/base/actions/workflows/docker-image-buster-armv7a.yml/badge.svg)](https://github.com/qtdocker/base/actions/workflows/docker-image-buster-armv7a.yml) 
#### Target arch:
- native: `docker pull atom63/qt-docker:linux-buster-armv7a`

#### Base arch: x86_64/amd [![Docker Image CI](https://github.com/qtdocker/base/actions/workflows/docker-image-buster-x86_64.yml/badge.svg)](https://github.com/qtdocker/base/actions/workflows/docker-image-buster-x86_64.yml)
#### Target arch:
- native: `docker pull atom63/qt-docker:linux-buster-x86_64`
- armv7a/armhf: `docker pull atom63/qt-docker:linux-buster-cross-x86_64-armv7a`

### Debian Bullseye
#### Base arch: armv7a/armhf [![Docker Image CI](https://github.com/qtdocker/base/actions/workflows/docker-image-bullseye-x86_64.yml/badge.svg)](https://github.com/qtdocker/base/actions/workflows/docker-image-bullseye-x86_64.yml) 
#### Target arch:
- native: `docker pull atom63/qt-docker:linux-bullseye-armv7a`

#### Base arch: x86_64/amd [![Docker Image CI](https://github.com/qtdocker/base/actions/workflows/docker-image-bullseye-armv7a.yml/badge.svg)](https://github.com/qtdocker/base/actions/workflows/docker-image-bullseye-armv7a.yml)
#### Target arch:
- native : `docker pull atom63/qt-docker:linux-bullseye-x86_64`
- armv7a/armhf: `docker pull atom63/qt-docker:linux-bullseye-cross-x86_64-armv7a`