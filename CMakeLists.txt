set(CMAKE_SYSTEM_NAME Generic)
set(CMAKE_TRY_COMPILE_TARGET_TYPE STATIC_LIBRARY)

cmake_minimum_required(VERSION 3.30)


project(Tutorial)

add_executable(tutorial)

target_sources(tutorial PRIVATE tutorial.c)

