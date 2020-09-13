cmake_minimum_required(VERSION 3.5)

SET(CMAKE_C_COMPILER "/usr/bin/clang")
SET(CMAKE_CXX_COMPILER "/usr/bin/clang++")

SET(CMAKE_EXPORT_COMPILE_COMMANDS TRUE)

project(android)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/build/cmake/")
list(APPEND CMAKE_PREFIX_PATH "${CMAKE_CURRENT_LIST_DIR}/build/cmake/config")

include(toolchain)
_get_host_tag(TAG)
toolchain_configure_tags(${TAG})

include(android)

set(ANDROID_QEMU2_TOP_DIR ${CMAKE_CURRENT_LIST_DIR}/)

prebuilt(Threads)

android_generate_hw_config()

add_definitions("-D__STDC_LIMIT_MACROS=1" "-D__STDC_FORMAT_MACROS=1")

include_directories(${ANDROID_QEMU2_TOP_DIR}/android-emu)
include_directories(${ANDROID_QEMU2_TOP_DIR}/android-emugl/host/include)
include_directories(${ANDROID_QEMU2_TOP_DIR}/android-emugl/shared)

add_subdirectory(${ANDROID_QEMU2_TOP_DIR}/astc-codec astc-codec)
add_subdirectory(android-emu)
add_subdirectory(android-emugl)