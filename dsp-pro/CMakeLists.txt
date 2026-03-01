CMAKE_MINIMUM_REQUIRED(VERSION 3.22)

project(DSP-PRO)

set(CMAKE_CXX_STANDARD 23)

set(LIB_DIR "${CMAKE_CURRENT_SOURCE_DIR}/libs")

include(cmake/cpm.cmake)

file(MAKE_DIRECTORY "${LIB_DIR}")

CPMAddPackage(
        NAME JUCE
        GITHUB_REPOSITORY juce-framework/JUCE
        GIT_TAG 8.0.12
        VERSION 8.0.12
        SOURCE_DIR ${LIB_DIR}/juce
)

CPMAddPackage(
        NAME GOOGLETEST
        GITHUB_REPOSITORY google/googletest
        VERSION 1.17.0
        SOURCE_DIR ${LIB_DIR}/googletest
        OPTIONS
            "INSTALL GTEST OFF"
            "gtest_force_shart_crt ON"
)

enable_testing()

if(MSVC)
    add_compile_options(/Wall /WX)
else()
    add_compile_options(-Wall -Wextra -Wpedantic)
endif()

add_subdirectory(bandpass_plugin)
add_subdirectory(test)