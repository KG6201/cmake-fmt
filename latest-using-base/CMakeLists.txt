cmake_minimum_required(VERSION 3.14)
project(latest-using-base CXX)
set(CMAKE_CXX_STANDARD 17)

include(CMakePrintHelpers)
cmake_print_variables(PROJECT_SOURCE_DIR)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)

cmake_path(GET PROJECT_SOURCE_DIR PARENT_PATH ROOT_DIR)
cmake_path(APPEND INCLUDE_DIR ${ROOT_DIR} include)
cmake_path(APPEND SOURCE_DIR ${ROOT_DIR} src)
cmake_print_variables(ROOT_DIR)
cmake_print_variables(INCLUDE_DIR)
cmake_print_variables(SOURCE_DIR)

add_executable(${PROJECT_NAME} main.cpp)

target_compile_options(${PROJECT_NAME} PRIVATE -O3 -Wall -Wextra -Wno-psabi)
target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_20)

include(FetchContent)
find_package(fmt 11.0.0)
FetchContent_Declare(
  fmt
  GIT_REPOSITORY https://github.com/fmtlib/fmt
  GIT_TAG        master
)
FetchContent_MakeAvailable(fmt)

target_link_libraries(${PROJECT_NAME} fmt::fmt)

