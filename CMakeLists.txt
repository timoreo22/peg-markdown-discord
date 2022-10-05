cmake_minimum_required(VERSION 3.22)
project(Peg-Markdown-Discord)

find_package(PkgConfig REQUIRED)
pkg_check_modules(GLIB2 REQUIRED glib-2.0 IMPORTED_TARGET)

add_subdirectory(peg-0.1.9)

add_custom_command(OUTPUT markdown_parser.c
        COMMAND ./peg-0.1.9/leg -o markdown_parser.c ${CMAKE_CURRENT_SOURCE_DIR}/markdown_parser.leg
        DEPENDS leg
        DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/markdown_parser.leg
        VERBATIM)
add_executable(${PROJECT_NAME} markdown.c markdown_parser.c markdown_output.c markdown_lib.c utility_functions.c parsing_functions.c odf.c)

add_library(markdown markdown_parser.c markdown_output.c markdown_lib.c utility_functions.c parsing_functions.c odf.c )


target_link_libraries(${PROJECT_NAME} PUBLIC PkgConfig::GLIB2)
target_link_libraries(markdown PUBLIC PkgConfig::GLIB2)

target_include_directories(${PROJECT_NAME} PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR})
target_include_directories(markdown PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR})