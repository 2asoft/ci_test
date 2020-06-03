cmake_minimum_required (VERSION 3.11)
project(hello_ci)

# Default debug and optimize flags.
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -DDEBUG")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -O3")

include_directories(${CMAKE_SOURCE_DIR})

add_subdirectory(src)
