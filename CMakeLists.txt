# Copyright (c) 2023 Advanced Micro Devices, Inc. All rights reserved.
if (DEFINED ENV{ROCM_PATH})
    set(ROCM_PATH "$ENV{ROCM_PATH}" CACHE STRING "ROCm install directory")
else()
    set(ROCM_PATH "/opt/rocm" CACHE STRING "ROCm install directory")
endif()
cmake_minimum_required(VERSION 3.5)
project(TransferBench CXX)
set( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3 -L${ROCM_PATH}/hsa/lib")
include_directories(${ROCM_PATH}/hsa/include)
link_libraries(numa hsa-runtime64)
set (CMAKE_RUNTIME_OUTPUT_DIRECTORY ..)
add_executable(TransferBench src/TransferBench.cpp)
target_include_directories(TransferBench PRIVATE src/include)

