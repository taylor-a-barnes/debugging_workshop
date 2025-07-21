cmake_minimum_required(VERSION 3.22)

# Project name and version
project(DebugExample VERSION 1.0
                     LANGUAGES CXX)

# Add the executable
add_executable(example src/main.cpp)

# Specify the C++ standard
target_compile_features(example PRIVATE cxx_std_11)

if(CMAKE_BUILD_TYPE STREQUAL "DEBUG")

  # Unfortunately, increasing the warnings level in CMake requires compiler-specific flags
  # Note: Before CMake 3.15, CMake applied the /W3 flag for MSVC automatically, so we would need to remove that
  target_compile_options(example PRIVATE
    $<$<CXX_COMPILER_ID:GNU,Clang>:-Wall -Wextra -Wpedantic>
    $<$<CXX_COMPILER_ID:MSVC>:/W4>
  )

  message(STATUS "Sanitizers ENABLED")
  set(SANITIZER_FLAGS "-fsanitize=address,leak,undefined -fno-omit-frame-pointer")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${SANITIZER_FLAGS}")
  set(CMAKE_LINKER_FLAGS "${CMAKE_LINKER_FLAGS} ${SANITIZER_FLAGS}")

endif()


