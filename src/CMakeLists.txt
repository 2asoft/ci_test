cmake_minimum_required (VERSION 3.11)
project(hello_ci)

# Default debug and optimize flags.
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -DDEBUG")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -O3")

include_directories(${CMAKE_SOURCE_DIR})

if (MSVC)
    add_compile_options ("$<$<CONFIG:DEBUG>:/RTCs>")
else ()
    add_compile_options (-g -fno-strict-aliasing -fno-strict-overflow -m32 -fshort-wchar -Werror=return-type -Werror=implicit-function-declaration -Werror=pointer-arith)

#    if (${CMAKE_BUILD_TYPE} STREQUAL "Debug")
#        add_compile_options (-O0)
#    else ()
#        add_compile_options (-O3)
#    endif ()
endif ()
include_directories (external/include)
link_directories (${PROJECT_SOURCE_DIR}/external/lib)
if (WIN32)
#    set (OPENAL_LIBRARIES openal)
#    set (OPENGL_LIBRARIES glew32 opengl32)
#    set (WIN32_LIBRARIES ws2_32 winmm)
elseif (APPLE)
#    set (OPENAL_LIBRARIES "-framework OpenAL")
#    set (OPENGL_LIBRARIES "-framework OpenGL")
else ()
#    set (OPENAL_LIBRARIES openal)
#    set (OPENGL_LIBRARIES GL)
#    set (PTHREAD_LIBRARIES pthread)
endif ()

add_executable (
    out

    main.cpp
)
target_link_libraries (
    out
#    SDL2
    "${OPENAL_LIBRARIES}"
    "${OPENGL_LIBRARIES}"
    "${PTHREAD_LIBRARIES}"
    "${WIN32_LIBRARIES}"
)
if (MSVC)
else ()
    target_link_options (out PUBLIC -m32)
endif ()
