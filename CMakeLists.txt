cmake_minimum_required(VERSION 3.4)
project(musashi)

add_executable(m68kmake
    m68kmake.c)

add_custom_command(
    OUTPUT  ${CMAKE_CURRENT_SOURCE_DIR}/m68kopac.c ${CMAKE_CURRENT_SOURCE_DIR}/m68kopdm.c ${CMAKE_CURRENT_SOURCE_DIR}/m68kopnz.c ${CMAKE_CURRENT_SOURCE_DIR}/m68kops.c ${CMAKE_CURRENT_SOURCE_DIR}/m68kops.h
    COMMAND m68kmake
    DEPENDS m68kmake
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
)

add_library(musashi
    m68kcpu.c
    m68kdasm.c

    ${CMAKE_CURRENT_SOURCE_DIR}/m68kopac.c
    ${CMAKE_CURRENT_SOURCE_DIR}/m68kopdm.c
    ${CMAKE_CURRENT_SOURCE_DIR}/m68kopnz.c
    ${CMAKE_CURRENT_SOURCE_DIR}/m68kops.c
    ${CMAKE_CURRENT_SOURCE_DIR}/m68kops.h
)

target_compile_definitions(musashi
    PUBLIC
        "M68K_COMPILE_FOR_MAME=OPT_OFF"
)

install(
    TARGETS musashi
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
)
