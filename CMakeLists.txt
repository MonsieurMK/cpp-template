cmake_minimum_required(VERSION 3.21)

set(PROJECT_NAME MyProject)

# --- Managing version ---
# 1. Get the latest git tag
execute_process(
    COMMAND git describe --tags --abbrev=0
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
    OUTPUT_VARIABLE GIT_TAG
    OUTPUT_STRIP_TRAILING_WHITESPACE
    ERROR_QUIET
)
# 2. Fallback if no tag exists or git is missing
if(NOT GIT_TAG)
    set(GIT_TAG "0.0.0-unknown")
endif()
# 3. (Optional) Extract just the numbers for CMake's VERSION field
# This turns "v0.1-domain-complete" into "0.1"
string(REGEX MATCH "([0-9]+\\.[0-9]+(\\.[0-9]+)?)" VERSION ${GIT_TAG})

project(${PROJECT_NAME}
  VERSION ${VERSION}
  LANGUAGES CXX
)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(INCLUDE_DIR ${PROJECT_SOURCE_DIR}/include)

add_subdirectory(src)

option(BUILD_TESTS "Build unit tests" ON)
if(BUILD_TESTS)
  add_subdirectory(test)
endif()
