cmake_minimum_required(VERSION 3.16)

project(ostis-example-app CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Find required packages
find_package(sc-machine REQUIRED)
find_package(scl-machine REQUIRED)
find_package(ps-common-lib REQUIRED)

# Set extensions output directory
set(SC_EXTENSIONS_DIRECTORY "${CMAKE_BINARY_DIR}/extensions")

# Include CMake modules
list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

# Code formatting
option(SC_CLANG_FORMAT_CODE "Format code with clang-format" OFF)
if(SC_CLANG_FORMAT_CODE)
    include(ClangFormat)
endif()

# Testing
option(SC_BUILD_TESTS "Build tests" OFF)
if(SC_BUILD_TESTS)
    enable_testing()
    find_package(GTest REQUIRED)
    include(tests)
endif()

# Add problem solver modules
add_subdirectory(problem-solver/cxx)
