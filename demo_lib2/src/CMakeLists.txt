# The Flutter tooling requires that developers have CMake 3.10 or later
# installed. You should not increase this version, as doing so will cause
# the plugin to fail to compile for some customers of the plugin.
cmake_minimum_required(VERSION 3.10)

project(demo_lib_library VERSION 0.0.1 LANGUAGES C)

add_library(demo_lib SHARED
  "demo_lib.c"
)

set_target_properties(demo_lib PROPERTIES
  PUBLIC_HEADER demo_lib.h
  OUTPUT_NAME "demo_lib"
)

target_compile_definitions(demo_lib PUBLIC DART_SHARED_LIB)

if (ANDROID)
  # Support Android 15 16k page size
  target_link_options(demo_lib PRIVATE "-Wl,-z,max-page-size=16384")
endif()
