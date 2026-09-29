cmake_minimum_required(VERSION 3.20)

project(minecraft_clone
    VERSION 0.1.0
    LANGUAGES CXX
)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

add_executable(minecraft_clone
    src/main.cpp
)

target_compile_options(minecraft_clone PRIVATE
    -Wall
    -Wextra
    -Wpedantic
)

# Make assets available from the build directory.
file(COPY assets DESTINATION ${CMAKE_BINARY_DIR})
