cmake_minimum_required(VERSION 3.22)

# Project name and version
project(DebugExample VERSION 1.0
                     LANGUAGES CXX)

# Add the executable
add_executable(example src/main.cpp)

# Specify the C++ standard
target_compile_features(example PRIVATE cxx_std_11)
