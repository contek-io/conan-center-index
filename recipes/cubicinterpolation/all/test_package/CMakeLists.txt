cmake_minimum_required(VERSION 3.1)
project(test_package LANGUAGES CXX)

find_package(CubicInterpolation REQUIRED CONFIG)

add_executable(${PROJECT_NAME} test_package.cpp)
target_link_libraries(${PROJECT_NAME} CubicInterpolation::CubicInterpolation)
set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 14)
