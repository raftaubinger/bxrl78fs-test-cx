set(CMAKE_SYSTEM_NAME Generic)
set(CMAKE_TRY_COMPILE_TARGET_TYPE STATIC_LIBRARY)

cmake_minimum_required(VERSION 3.30)

project(Tutorial)

add_executable(tutorial)

target_sources(tutorial PRIVATE tutorial.c)

target_link_options(tutorial PRIVATE
  -D_NEAR_HEAP_SIZE=0
  -D_FAR_HEAP_SIZE=0
  -D_HUGE_HEAP_SIZE=0
  -D_STACK_SIZE=128
  -D_NEAR_CONST_LOCATION_SIZE=0xCF00
)
