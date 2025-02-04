cmake_minimum_required(VERSION 3.20...3.31 FATAL_ERROR)

project(MD5 LANGUAGES CXX)

add_library(MD5 STATIC
        src/md5.cpp
        src/md5.h
        src/md5_loc.h)

if(CMAKE_CXX_BYTE_ORDER STREQUAL "BIG_ENDIAN")
    set(MD5_BIG_ENDIAN ON)
endif()

option(MD5_DEBUG "Enable MD5 debug" OFF)
option(MD5_SYSTEM_HEADERS "Mark MD5 headers as SYSTEM" OFF)
if(MD5_SYSTEM_HEADERS)
    set(_md5_maybe_system "SYSTEM")
endif()

configure_file(src/conf.h.in conf.h)
target_include_directories(MD5 PRIVATE "${CMAKE_CURRENT_BINARY_DIR}")

target_include_directories(MD5 ${_md5_maybe_system} INTERFACE src)