cmake_minimum_required(VERSION 3.23.2)

project(quickjs)

set(CMAKE_C_STANDARD 23)

file(STRINGS _VERSION VERSION)

add_library(qjs-core quickjs.c libregexp.c libunicode.c cutils.c quickjs-libc.c libbf.c)
target_compile_definitions(qjs-core PUBLIC
        CONFIG_BIGNUM=y
        CONFIG_VERSION="${VERSION}"
        _GNU_SOURCE
)
target_include_directories(qjs-core PUBLIC ${quickjs_SOURCE_DIR})