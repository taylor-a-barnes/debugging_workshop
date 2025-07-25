cmake_minimum_required(VERSION 3.22)

# Project name and version
project(MDExample VERSION 1.0
  LANGUAGES CXX)

# Add the executable
add_executable(md src/main.cpp)

# Specify the C++ standard
target_compile_features(md PRIVATE cxx_std_11)

# Increase the warning level
target_compile_options(md PRIVATE
  $<$<AND:$<CONFIG:Debug>,$<CXX_COMPILER_ID:GNU,Clang>>:-Wall;-Wextra;-Wpedantic>
  $<$<AND:$<CONFIG:Debug>,$<CXX_COMPILER_ID:MSVC>>:/W4>
)

# Enable santizers
target_compile_options(md PRIVATE
  $<$<AND:$<CONFIG:Debug>,$<CXX_COMPILER_ID:GNU,Clang>>:-fsanitize=address,undefined;-fno-omit-frame-pointer>
  $<$<AND:$<CONFIG:Debug>,$<CXX_COMPILER_ID:MSVC>>:/fsanitize=address;/Zi;/Od>
)
target_link_options(md PRIVATE
  $<$<AND:$<CONFIG:Debug>,$<CXX_COMPILER_ID:GNU,Clang>>:-fsanitize=address,undefined;-fno-omit-frame-pointer>
  $<$<AND:$<CONFIG:Debug>,$<CXX_COMPILER_ID:MSVC>>:/INCREMENTAL:NO;/fsanitize=address>
)

