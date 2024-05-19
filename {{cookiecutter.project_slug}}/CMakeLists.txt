cmake_minimum_required(VERSION 3.15)

if(DEFINED ENV{VCPKG_ROOT} AND NOT DEFINED CMAKE_TOOLCHAIN_FILE)
  message(STATUS "VCPKG_ROOT: $ENV{VCPKG_ROOT}")
  set(CMAKE_TOOLCHAIN_FILE "$ENV{VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake")
else()
  set(CMAKE_TOOLCHAIN_FILE "${CMAKE_CURRENT_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake" CACHE STRING "Vcpkg toolchain file")
endif()

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake")

add_compile_options("$<$<C_COMPILER_ID:MSVC>:/utf-8>")
add_compile_options("$<$<CXX_COMPILER_ID:MSVC>:/utf-8>")

project({{ cookiecutter.project_slug }} VERSION 1.0)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED True)

add_executable(${PROJECT_NAME} src/main.cc)

find_package(Drogon CONFIG REQUIRED)

target_link_libraries(${PROJECT_NAME} PRIVATE Drogon::Drogon)

target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_23)
