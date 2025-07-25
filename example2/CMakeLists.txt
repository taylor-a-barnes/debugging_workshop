cmake_minimum_required(VERSION 3.22)

# Project name and version
project(DebugExample VERSION 1.0
                     LANGUAGES CXX)

# Add the executable
add_executable(example src/main.cpp)

# Specify the C++ standard
target_compile_features(example PRIVATE cxx_std_11)

# Increase the warning level
target_compile_options(example PRIVATE
  $<$<AND:$<CONFIG:Debug>,$<CXX_COMPILER_ID:GNU,Clang>>:-Wall;-Wextra;-Wpedantic>
  $<$<AND:$<CONFIG:Debug>,$<CXX_COMPILER_ID:MSVC>>:/W4>
)
