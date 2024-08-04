# GLU (OpenGL Utilities Library)
The source code is published from the [Mesa 3D Library](https://archive.mesa3d.org/glu/) as-is without any functional modifications. Current repository aims to make the library available using the VCPKG package manager.

## How to use this in your projects?
`vcpkg.json` file:

```json
{
  "$schema": "https://raw.githubusercontent.com/microsoft/vcpkg-tool/main/docs/vcpkg.schema.json",
  "dependencies": [
    "glu"
  ]
}
```

`vcpkg-configuration.json` file:
```json
{
  "$schema": "https://raw.githubusercontent.com/microsoft/vcpkg-tool/main/docs/vcpkg-configuration.schema.json",
  "default-registry": {
    "kind": "git",
    "baseline": "7f9f0e44db287e8e67c0e888141bfa200ab45121",
    "repository": "https://github.com/microsoft/vcpkg"
  },
  "registries": [
    {
      "kind": "git",
      "repository": "https://github.com/sachingodishela/vcpkg-registry",
      "baseline": "8c4d521ce5ff80e7a2d177bb397f01cac5db90cf",
      "packages": ["glu"]
    }
  ]
}
```

`CMakeLists.txt` file:
```
find_package(GLU REQUIRED)
```
