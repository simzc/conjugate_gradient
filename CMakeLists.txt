cmake_minimum_required(VERSION 3.25.0 FATAL_ERROR)

project(conjugate_gradient LANGUAGES CXX CUDA)

find_package(CUDAToolkit REQUIRED)
include_directories(${CMAKE_CUDA_TOOLKIT_INCLUDE_DIRECTORIES})
include_directories(/opt/cuda-samples-12.0/Common)

add_executable(
    conjugate_gradient
    main.cu
)

target_link_libraries(
    conjugate_gradient
    CUDA::cusparse
    CUDA::cublas
)

# set_target_properties(conjugate_gradient PROPERTIES LINKER_LANGUAGE CUDA)