cmake_minimum_required(VERSION 3.14)
project(CLion)

set(CMAKE_CXX_STANDARD 14)

add_executable(CLion
        forward.cpp
        forward.h
        main.cpp
        )

list(APPEND CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake)


find_package(ARIA)

target_include_directories(CLion PUBLIC ${ARIA_INCLUDE_DIRS})

target_link_libraries(CLion PUBLIC ${ARIA_LIBRARIES})