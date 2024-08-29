set(CMAKE_SYSTEM_NAME Generic)
set(CMAKE_TRY_COMPILE_TARGET_TYPE STATIC_LIBRARY)

cmake_minimum_required(VERSION 3.30)

project(Tutorial LANGUAGES C)

set(TOOLKIT_DIR /opt/iarsystems/bxrl78fs/rl78)

add_executable(tutorial)

target_sources(tutorial PRIVATE tutorial.c)

target_link_options(tutorial PRIVATE
  "SHELL:
  --config_def _NEAR_HEAP_SIZE=0
  --config_def _FAR_HEAP_SIZE=0
  --config_def _HUGE_HEAP_SIZE=0
  --config_def _STACK_SIZE=128
  --config_def _NEAR_CONST_LOCATION_START=0x2000
  --config_def _NEAR_CONST_LOCATION_SIZE=0xC000"
  --define_symbol _NEAR_CONST_LOCATION=0
  --config ${TOOLKIT_DIR}/config/lnkrl78_s3.icf
  --debug_lib
)

# Convert the ELF output to .hex
function(iar_elf_tool_hex TARGET)
  add_custom_command(TARGET ${TARGET} POST_BUILD COMMAND ${CMAKE_IAR_ELFTOOL} --silent --ihex $<TARGET_FILE:${TARGET}> $<IF:$<BOOL:$<TARGET_PROPERTY:${TARGET},OUTPUT_NAME>>,$<TARGET_PROPERTY:${TARGET},OUTPUT_NAME>,$<TARGET_PROPERTY:${TARGET},NAME>>.hex)
endfunction()

iar_elf_tool_hex(tutorial)

