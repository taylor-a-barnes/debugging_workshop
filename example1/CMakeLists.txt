cmake_minimum_required(VERSION 3.22)

# Project name and version
project(DebugExample VERSION 1.0
                     LANGUAGES CXX)

# Add the executable
add_executable(example src/main.cpp)

# Specify the C++ standard
target_compile_features(example PRIVATE cxx_std_11)

# Unfortunately, increasing the warnings level in CMake requires compiler-specific flags
# Note: Before CMake 3.15, CMake applied the /W3 flag for MSVC automatically, so we would need to remove that
#if(CMAKE_BUILD_TYPE STREQUAL "DEBUG") # If using a multiconfiguration generator, CMAKE_BUILD_TYPE is not known as configure time
#  if(MSVC)
#    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /W4") # This sets a global flag, which is not ideal
#  else()
#    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -Wpedantic") # Also sets a global flag
#  endif()
#endif()

# Increase the warning level
target_compile_options(example PRIVATE
  $<$<AND:$<CONFIG:Debug>,$<CXX_COMPILER_ID:GNU,Clang>>:-Wall;-Wextra;-Wpedantic>
  $<$<AND:$<CONFIG:Debug>,$<CXX_COMPILER_ID:MSVC>>:/W4>
)

