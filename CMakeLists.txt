cmake_minimum_required(VERSION 3.10)

################################
## Project
################################
project(tinycbor)

set(PROJECT_VERSION_MAJOR "0")
set(PROJECT_VERSION_MINOR "5")
set(PROJECT_VERSION_PATCH "2")
set(PROJECT_VERSION "${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}.${PROJECT_VERSION_PATCH}")

message("\n-- Configuring ${PROJECT_NAME} ${PROJECT_VERSION}...\n")

################################
## Cmake dependencies
################################
set(CMAKE_VERBOSE_MAKEFILE ON)
set(CMAKE_COLOR_MAKEFILE ON)
set(CMAKE_DISABLE_IN_SOURCE_BUILD ON)
set(CMAKE_DISABLE_SOURCE_CHANGES ON)

include(GNUInstallDirs)

################################
## Compiler Flags
################################

################################
## Dependencies
################################

################################
# Library Sources
################################
# src
set(TINY_CBOR_SOURCES
        src/cborerrorstrings.c
        src/cborencoder.c
        src/cborencoder_close_container_checked.c
        src/cborparser.c
        src/cborpretty.c
        src/cborparser_dup_string.c
        src/cborpretty_stdio.c
        src/cbortojson.c
        src/cborvalidation.c
        src/open_memstream.c)

################################
# Library Build
################################
add_library(tinycbor ${TINY_CBOR_SOURCES})
target_include_directories(tinycbor
        PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include>
        PRIVATE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>
        $<INSTALL_INTERFACE:src>)

################################
## Install
################################
# 'make install' to the correct locations (provided by GNUInstallDirs).
install(TARGETS tinycbor EXPORT tinycbor-config
        ARCHIVE DESTINATION lib
        LIBRARY DESTINATION lib
        RUNTIME DESTINATION bin)  # This is for Windows
install(DIRECTORY include/ DESTINATION include/tinycbor)
install(EXPORT tinycbor-config DESTINATION share/tinycbor/cmake)
export(TARGETS tinycbor FILE tinycbor-config.cmake)

################################
#
################################
add_subdirectory(tools)
################################
## Test
################################
enable_testing()
add_subdirectory(tests)