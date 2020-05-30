cmake_minimum_required(VERSION 3.1)

project(Texturing)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif()

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED yes)

# Compiler flags
if(CMAKE_CXX_COMPILER_ID STREQUAL "MSVC")
    add_compile_options(/W3)
elseif(CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
    add_compile_options(-Wall -Wextra -Wundef -pedantic)
    add_compile_options(-mpopcnt)
elseif(CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
    add_compile_options(-Weverything -pedantic)
endif()

if(WIN32)
    add_definitions(-DWIN32_LEAN_AND_MEAN -DVC_EXTRALEAN -DNOMINMAX)
    add_definitions(-D_CRT_SECURE_NO_WARNINGS)
    if(MSVC)
        add_compile_options(/MP)
        option(MVE_BUILD_WITH_SSE2 "Build MVE with SSE2 support" ON)
        option(MVE_BUILD_WITH_SSE3 "Build MVE with SSE3 support" ON)
        if(MVE_BUILD_WITH_SSE2)
            add_definitions(-D__SSE2__)
        endif()
        if(MVE_BUILD_WITH_SSE3)
            add_definitions(-D__SSE3__)
        endif()
    endif()

endif()

find_package(OpenMP REQUIRED)
#add_compile_options(${OpenMP_CXX_FLAGS})
if(OPENMP_FOUND)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_EXE_LINKER_FLAGS}")
endif()

find_package(JPEG REQUIRED)
find_package(PNG REQUIRED)
find_package(TIFF REQUIRED)
find_package(Eigen3 REQUIRED)
find_package(TBB REQUIRED)

include_directories(SYSTEM
    ${CMAKE_SOURCE_DIR}/libs/mapmap/
    ${CMAKE_SOURCE_DIR}/libs/mapmap/mapmap
    ${CMAKE_SOURCE_DIR}/libs/mapmap/ext/dset
)

include_directories(libs)

add_subdirectory(libs)
add_subdirectory(apps)