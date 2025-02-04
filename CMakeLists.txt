cmake_minimum_required(VERSION 3.20...3.31 FATAL_ERROR)

add_library(MD5 STATIC
        src/md5.cpp
        src/md5.h
        src/md5_loc.h)

if(CMAKE_CXX_BYTE_ORDER STREQUAL "BIG_ENDIAN")
    target_compile_definitions(MD5 PUBLIC MD5_BIG_ENDIAN=1)
else()
    target_compile_definitions(MD5 PUBLIC MD5_BIG_ENDIAN=0)
endif()

option(MD5_DEBUG "Enable MD5 debug" OFF)
if(MD5_DEBUG)
    target_compile_definitions(MD5 PUBLIC MD5_DEBUG=1)
else()
    target_compile_definitions(MD5 PUBLIC MD5_DEBUG=0)
endif()

target_include_directories(MD5 INTERFACE src)
