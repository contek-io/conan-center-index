cmake_minimum_required(VERSION 3.1)
project(test_package LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(OpenCLHeadersCpp REQUIRED CONFIG)

add_library(${PROJECT_NAME} OBJECT test_package.cpp)
target_link_libraries(${PROJECT_NAME} PRIVATE OpenCL::HeadersCpp)
