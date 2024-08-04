# GLU (OpenGL Utilities Library)
The source code is published from the [Mesa 3D Library](https://archive.mesa3d.org/glu/) as-is without any functional modifications. Current repository aims to make the library available using the VCPKG package manager.

## How to use this in your projects?
1. In vcpkg.json manifest file, add `GLU` in the list of dependencies.
2. In CMakeLists.txt file, add `find_package(GLU)`.
