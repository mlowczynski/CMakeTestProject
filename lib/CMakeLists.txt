# Minimum version, that supports all features used
cmake_minimum_required(VERSION 3.26)
project(MyLibrary VERSION 1.0.0)

# I prefer to use PROJECT_NAME variable where possible
add_library("${PROJECT_NAME}" SHARED "${CMAKE_CURRENT_SOURCE_DIR}/src/MyLibrary.cpp")
add_library("${PROJECT_NAME}::${PROJECT_NAME}" ALIAS "${PROJECT_NAME}")

# "adds" CppGenerator
add_subdirectory(generators)

# define dependency
add_dependencies("${PROJECT_NAME}" CppGenerator)

# sets shared library properties, creates SOVERSION symlinks
set_target_properties(
        "${PROJECT_NAME}" PROPERTIES
        VERSION "${PROJECT_VERSION}"
        SOVERSION "${PROJECT_VERSION_MAJOR}"
)

# get include directories of generated sources
get_target_property(CppGenerator_INCLUDE_DIRECTORIES CppGenerator INCLUDE_DIRECTORIES)

target_include_directories(
        "${PROJECT_NAME}" INTERFACE
        INTERFACE "${CMAKE_CURRENT_SOURCE_DIR}/src"
        PRIVATE "${CppGenerator_INCLUDE_DIRECTORIES}"
)
