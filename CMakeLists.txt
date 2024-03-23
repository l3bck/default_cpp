cmake_minimum_required(VERSION 3.16)

project(default_cpp)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

include_directories(${PROJECT_SOURCE_DIR}/src)
include_directories(${PROJECT_SOURCE_DIR}/test)

add_subdirectory(libs)
add_subdirectory(src)
add_subdirectory(test)



if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
    set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS} -fopenmp -Wall -Wextra -Werror -std=c++20 -flto -ffat-lto-objects -O3")
    set(CMAKE_EXE_LINKER_FLAGS_RELEASE "${CMAKE_EXE_LINKER_FLAGS} -fuse-linker-plugin")
elseif(CMAKE_COMPILER_IS_GNUCXX)
    set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS} -fopenmp=libomp -Wall -Wextra -Werror -std=c++20 -flto -ffat-lto-objects -O3")
    set(CMAKE_EXE_LINKER_FLAGS_RELEASE "${CMAKE_EXE_LINKER_FLAGS} -fuse-linker-plugin")
elseif (MSVC)
endif()

if ("${CMAKE_BUILD_TYPE}" STREQUAL "")
message("-- Default release build")
set(CMAKE_BUILD_TYPE "Release")
endif()

message("-- Build type: " ${CMAKE_BUILD_TYPE})