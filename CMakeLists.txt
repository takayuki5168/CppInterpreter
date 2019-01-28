# cmake version
cmake_minimum_required(VERSION 3.0)

# project name
project(CppInterpreter CXX C)

# Compiler
include(CheckCXXCompilerFlag)
CHECK_CXX_COMPILER_FLAG("-std=gnu++14" COMPILER_SUPPORTS_CXX14)
if(COMPILER_SUPPORTS_CXX14)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++14")
else()
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++11")
endif()

# linenoise
set(LINENOISE_INCLUDE_DIR ${CMAKE_CURRENT_LIST_DIR}/external/linenoise)
include_directories(SYSTEM ${LINENOISE_INCLUDE_DIR})
file(GLOB LINENOISE_SOURCE ${CMAKE_CURRENT_LIST_DIR}/external/linenoise/*.c)
add_library(LINENOISE STATIC ${LINENOISE_SOURCE})

# CppInterpreter
#file(GLOB_RECURSE LIB_SOURCES ${CMAKE_CURRENT_LIST_DIR}/lib/src/core/*.cpp)
#include_directories(LIB_HEADERS ${CMAKE_CURRENT_LIST_DIR}/lib/include/)

# main
file(GLOB MAIN_SOURCE main.cpp) 
add_executable(main
  ${MAIN_SOURCE})
target_link_libraries(main
  LINENOISE
  pthread)
