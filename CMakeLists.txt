# SPDX-License-Identifier: MIT
# Copyright © 2021 Intel Corporation

cmake_minimum_required(VERSION 3.10)

# Set project name and version
project(GLU VERSION 1.3.1 LANGUAGES C CXX)

# Define the list of source files
set(SOURCES
    libutil/error.c
    libutil/glue.c
    libutil/mipmap.c
    libutil/project.c
    libutil/quad.c
    libutil/registry.c
    libtess/dict.c
    libtess/geom.c
    libtess/memalloc.c
    libtess/mesh.c
    libtess/normal.c
    libtess/priorityq.c
    libtess/render.c
    libtess/sweep.c
    libtess/tess.c
    libtess/tessmono.c
    libnurbs/interface/bezierEval.cc
    libnurbs/interface/bezierPatch.cc
    libnurbs/interface/bezierPatchMesh.cc
    libnurbs/interface/glcurveval.cc
    libnurbs/interface/glinterface.cc
    libnurbs/interface/glrenderer.cc
    libnurbs/interface/glsurfeval.cc
    libnurbs/interface/incurveeval.cc
    libnurbs/interface/insurfeval.cc
    libnurbs/internals/arc.cc
    libnurbs/internals/arcsorter.cc
    libnurbs/internals/arctess.cc
    libnurbs/internals/backend.cc
    libnurbs/internals/basiccrveval.cc
    libnurbs/internals/basicsurfeval.cc
    libnurbs/internals/bin.cc
    libnurbs/internals/bufpool.cc
    libnurbs/internals/cachingeval.cc
    libnurbs/internals/ccw.cc
    libnurbs/internals/coveandtiler.cc
    libnurbs/internals/curve.cc
    libnurbs/internals/curvelist.cc
    libnurbs/internals/curvesub.cc
    libnurbs/internals/dataTransform.cc
    libnurbs/internals/displaylist.cc
    libnurbs/internals/flist.cc
    libnurbs/internals/flistsorter.cc
    libnurbs/internals/hull.cc
    libnurbs/internals/intersect.cc
    libnurbs/internals/knotvector.cc
    libnurbs/internals/mapdesc.cc
    libnurbs/internals/mapdescv.cc
    libnurbs/internals/maplist.cc
    libnurbs/internals/mesher.cc
    libnurbs/internals/monoTriangulationBackend.cc
    libnurbs/internals/monotonizer.cc
    libnurbs/internals/mycode.cc
    libnurbs/internals/nurbsinterfac.cc
    libnurbs/internals/nurbstess.cc
    libnurbs/internals/patch.cc
    libnurbs/internals/patchlist.cc
    libnurbs/internals/quilt.cc
    libnurbs/internals/reader.cc
    libnurbs/internals/renderhints.cc
    libnurbs/internals/slicer.cc
    libnurbs/internals/sorter.cc
    libnurbs/internals/splitarcs.cc
    libnurbs/internals/subdivider.cc
    libnurbs/internals/tobezier.cc
    libnurbs/internals/trimline.cc
    libnurbs/internals/trimregion.cc
    libnurbs/internals/trimvertpool.cc
    libnurbs/internals/uarray.cc
    libnurbs/internals/varray.cc
    libnurbs/nurbtess/directedLine.cc
    libnurbs/nurbtess/gridWrap.cc
    libnurbs/nurbtess/monoChain.cc
    libnurbs/nurbtess/monoPolyPart.cc
    libnurbs/nurbtess/monoTriangulation.cc
    libnurbs/nurbtess/partitionX.cc
    libnurbs/nurbtess/partitionY.cc
    libnurbs/nurbtess/polyDBG.cc
    libnurbs/nurbtess/polyUtil.cc
    libnurbs/nurbtess/primitiveStream.cc
    libnurbs/nurbtess/quicksort.cc
    libnurbs/nurbtess/rectBlock.cc
    libnurbs/nurbtess/sampleComp.cc
    libnurbs/nurbtess/sampleCompBot.cc
    libnurbs/nurbtess/sampleCompRight.cc
    libnurbs/nurbtess/sampleCompTop.cc
    libnurbs/nurbtess/sampleMonoPoly.cc
    libnurbs/nurbtess/sampledLine.cc
    libnurbs/nurbtess/searchTree.cc
)

# Add the library
add_library(GLU STATIC ${SOURCES})

# Define the include directories
include_directories(
    ${CMAKE_SOURCE_DIR}/include
    ${CMAKE_SOURCE_DIR}/libnurbs/internals
    ${CMAKE_SOURCE_DIR}/libnurbs/interface
    ${CMAKE_SOURCE_DIR}/libnurbs/nurbtess
)

# Set the compile options
target_compile_definitions(GLU PRIVATE LIBRARYBUILD)

# Set the C++ standard
set_target_properties(GLU PROPERTIES
    CXX_STANDARD 11
    CXX_STANDARD_REQUIRED ON
)

# Set visibility to hidden
set_target_properties(GLU PROPERTIES
    COMPILE_OPTIONS "-fvisibility=hidden"
)

# Link dependencies (you need to define `dep_gl` elsewhere or find a suitable CMake package)
# target_link_libraries(GLU PRIVATE ${dep_gl})

# Set version
set_target_properties(GLU PROPERTIES VERSION 1.3.1 SOVERSION 1)

# Installation rules
install(TARGETS GLU DESTINATION lib)
install(DIRECTORY include/ DESTINATION include)

# For subproject users
add_library(glu::GLU ALIAS GLU)

install(FILES include/GL/glu.h DESTINATION include/GL)

# Configure pkg-config file
include(CMakePackageConfigHelpers)

write_basic_package_version_file(
    "${CMAKE_CURRENT_BINARY_DIR}/glu-config-version.cmake"
    VERSION ${PROJECT_VERSION}
    COMPATIBILITY SameMajorVersion
)

configure_package_config_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/glu-config.cmake.in"
    "${CMAKE_CURRENT_BINARY_DIR}/glu-config.cmake"
    INSTALL_DESTINATION lib/cmake/glu
)

install(
    FILES
        "${CMAKE_CURRENT_BINARY_DIR}/glu-config.cmake"
        "${CMAKE_CURRENT_BINARY_DIR}/glu-config-version.cmake"
    DESTINATION lib/cmake/glu
)

# Export target for use in other projects
export(TARGETS GLU FILE "${CMAKE_CURRENT_BINARY_DIR}/glu-targets.cmake")

# Optionally include the generated CMake configuration files
include(CMakePackageConfigHelpers)
