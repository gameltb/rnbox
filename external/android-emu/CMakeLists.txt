project(android-emu)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/build/cmake/")
include(toolchain)
_get_host_tag(TAG)
toolchain_configure_tags(${TAG})

include(android)

set(ANDROID_QEMU2_TOP_DIR ${CMAKE_CURRENT_LIST_DIR}/)

add_subdirectory(${ANDROID_QEMU2_TOP_DIR}/astc-codec astc-codec)
add_subdirectory(android-emu)
add_subdirectory(android-emugl)