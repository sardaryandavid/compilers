cmake_minimum_required(VERSION 3.13.4)
project(RPO)

set(LT_LLVM_INSTALL_DIR "" CACHE PATH "LLVM installation directory")
list(APPEND CMAKE_PREFIX_PATH "${LT_LLVM_INSTALL_DIR}/lib/cmake/llvm/")
find_package(LLVM 15 REQUIRED CONFIG)
include_directories(SYSTEM ${LLVM_INCLUDE_DIRS})

set(CMAKE_CXX_STANDARD 17 CACHE STRING "")

if(NOT LLVM_ENABLE_RTTI)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fno-rtti")
endif()

add_library(RPO SHARED ../src/rpo.cpp)
target_link_libraries(RPO
  "$<$<PLATFORM_ID:Darwin>:-undefined dynamic_lookup>")