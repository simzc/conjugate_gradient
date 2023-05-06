cmake_minimum_required(VERSION 3.25.0 FATAL_ERROR)

project(conjugate_gradient LANGUAGES CXX CUDA)

find_package(CUDAToolkit REQUIRED)
include_directories(${CMAKE_CUDA_TOOLKIT_INCLUDE_DIRECTORIES})
include_directories(/opt/cuda-samples-12.0/Common)

option(cublas_test "test cublas" OFF)
option(cubsparse_test "test cusparse" OFF)
option(cubsparse_inp "test cusparse_inp" ON)

if(cublas_test)
    set(SRC_FILES cublas_test.cu)
endif()

if(cubsparse_test)
    set(SRC_FILES cusparse_test.cu)
endif()

if(cubsparse_inp)
    set(SRC_FILES cusparse_inp.cu)
endif()

add_executable(
    conjugate_gradient
    ${SRC_FILES}
)

target_link_libraries(
    conjugate_gradient
    CUDA::cusparse
    CUDA::cublas
)

# set_target_properties(conjugate_gradient PROPERTIES LINKER_LANGUAGE CUDA)