cmake_minimum_required(VERSION 2.8)
project(osg-dae)
set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}")

include(FindPkgConfig)
pkg_check_modules(OSG REQUIRED openscenegraph-osg)
pkg_check_modules(XML REQUIRED libxml-2.0)
include(OsgMacroUtils)
find_package(FBX REQUIRED)

if (NOT FBX_FOUND)
    message(FATAL_ERROR "could not find the FBX SDK")
endif()
add_subdirectory(src)
