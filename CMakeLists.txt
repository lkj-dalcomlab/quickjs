cmake_minimum_required(VERSION 3.23.2)

project(quickjs)

set(CMAKE_C_STANDARD 23)

#add_library(qjs-engine libregexp.c libunicode.c cutils.c quickjs-libc.c libbf.c)
#target_compile_definitions( qjs-engine PUBLIC
#        CONFIG_BIGNUM=y
#        CONFIG_VERSION="2020-11-08"
#        _GNU_SOURCE
#        )
#
#add_executable(qjsc qjsc.c)
#target_link_libraries(qjsc qjs-engine)

file(STRINGS VERSION VERSION)

include_directories( ${quickjs_SOURCE_DIR}/ )
message([TRACE] " quickjs source = ${quickjs_SOURCE_DIR} ")

file(GLOB quickjs_hpp ${quickjs_SOURCE_DIR}/*.h )

file(GLOB quickjs_src ${quickjs_SOURCE_DIR}/quickjs.c
        ${quickjs_SOURCE_DIR}/libregexp.c
        ${quickjs_SOURCE_DIR}/libunicode.c
        ${quickjs_SOURCE_DIR}/cutils.c
        ${quickjs_SOURCE_DIR}/quickjs-libc.c
        ${quickjs_SOURCE_DIR}/libbf.c
        )


add_library( qjs-engine ${quickjs_src} ${quickjs_hpp} )
target_compile_options( qjs-engine PRIVATE
        -MMD -MF
        -Wno-sign-compare
        -Wno-missing-field-initializers
        -Wundef -Wuninitialized
        -Wundef -Wuninitialized -Wwrite-strings -Wchar-subscripts
        )
target_compile_definitions( qjs-engine PUBLIC
        CONFIG_BIGNUM=y
        CONFIG_VERSION="${VERSION}"
        _GNU_SOURCE
        )

#add_executable(qjsc ${quickjs_SOURCE_DIR}/qjsc.c )
#target_compile_definitions( qjsc  PUBLIC  CONFIG_BIGNUM=y  CONFIG_VERSION="${VERSION}" _GNU_SOURCE )
#target_link_libraries( qjsc  qjs-engine )

#install(TARGETS qjsc DESTINATION ${quickjs_SOURCE_DIR})
#
#execute_process(COMMAND ${quickjs_SOURCE_DIR}/qjsc -c -o ../repl.c -m ../repl.js)
#execute_process(COMMAND ${quickjs_SOURCE_DIR}/qjsc -fbignum -c -o ../qjscalc.c ../qjscalc.js)
#
#add_executable(qjs qjs.c repl.c qjscalc.c)
#target_link_libraries(qjs qjs-engine)