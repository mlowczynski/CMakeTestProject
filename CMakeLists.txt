cmake_minimum_required(VERSION 3.26)
project(MyExecutable VERSION 1.0.0)

# "adds" MyLibrary
add_subdirectory(lib)

# I prefer to use PROJECT_NAME variable where possible
add_executable("${PROJECT_NAME}" "${CMAKE_CURRENT_SOURCE_DIR}/src/main.cpp")

# define dependency
add_dependencies("${PROJECT_NAME}" MyLibrary::MyLibrary)

target_link_libraries(
        "${PROJECT_NAME}" PRIVATE
        MyLibrary::MyLibrary
)
