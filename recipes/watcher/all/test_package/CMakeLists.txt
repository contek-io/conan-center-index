cmake_minimum_required(VERSION 3.12)

project(test_package LANGUAGES CXX)

find_package(watcher REQUIRED CONFIG)
find_package(Threads REQUIRED)

add_executable(${PROJECT_NAME} test_package.cpp)
target_link_libraries(${PROJECT_NAME} PRIVATE watcher::watcher Threads::Threads)
target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_20)
if(watcher_VERSION VERSION_LESS "0.4.0")
    target_compile_definitions(${PROJECT_NAME} PRIVATE WATCHER_NAMESPACE=water)
    target_compile_definitions(${PROJECT_NAME} PRIVATE WATCHER_EVENT_NAMESPACE=water::watcher::event)
    target_compile_definitions(${PROJECT_NAME} PRIVATE WATCHER_EVENT_KIND_NAMESPACE=water::watcher::event)
else()
    target_compile_definitions(${PROJECT_NAME} PRIVATE WATCHER_NAMESPACE=wtr)
    if(watcher_VERSION VERSION_LESS "0.8.1")
        target_compile_definitions(${PROJECT_NAME} PRIVATE WATCHER_EVENT_NAMESPACE=wtr::watcher::event)
        target_compile_definitions(${PROJECT_NAME} PRIVATE WATCHER_EVENT_KIND_NAMESPACE=wtr::watcher::event)
    else()
        target_compile_definitions(${PROJECT_NAME} PRIVATE WATCHER_EVENT_NAMESPACE=wtr::watcher)
        target_compile_definitions(${PROJECT_NAME} PRIVATE WATCHER_EVENT_KIND_NAMESPACE=wtr::watcher::event)
    endif()
endif()

if(watcher_VERSION VERSION_GREATER_EQUAL "0.6.0")
    target_compile_definitions(${PROJECT_NAME} PRIVATE WATCHER_WATCH_OBJECT)
elseif(watcher_VERSION VERSION_GREATER_EQUAL "0.5.0")
    target_compile_definitions(${PROJECT_NAME} PRIVATE WATCHER_DIE_WITH_PATH)
endif()
