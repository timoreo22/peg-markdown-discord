cmake_minimum_required(VERSION 3.22)
project(peg)
if(EXISTS ${CMAKE_CURRENT_BINARY_DIR}/leg)
    add_custom_command(OUTPUT leg.c
            COMMAND ${CMAKE_CURRENT_BINARY_DIR}/leg -o ${CMAKE_CURRENT_SOURCE_DIR}/leg.c ${CMAKE_CURRENT_SOURCE_DIR}/leg.leg
            DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/leg.leg
            VERBATIM)
endif()
if(EXISTS ${CMAKE_CURRENT_BINARY_DIR}/peg)
    add_custom_command(OUTPUT peg.peg-c
            COMMAND ${CMAKE_CURRENT_BINARY_DIR}/peg -o ${CMAKE_CURRENT_SOURCE_DIR}/peg.peg-c ${CMAKE_CURRENT_SOURCE_DIR}/peg.peg
            DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/peg.peg
            VERBATIM)
endif()
add_executable(peg peg.c ${CMAKE_CURRENT_SOURCE_DIR}/peg.peg-c tree.c compile.c)
add_executable(leg ${CMAKE_CURRENT_SOURCE_DIR}/leg.c tree.c compile.c)
target_include_directories(peg PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR})
target_include_directories(leg PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR})