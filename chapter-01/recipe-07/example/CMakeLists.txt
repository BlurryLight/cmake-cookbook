# set minimum cmake version
cmake_minimum_required(VERSION 3.5 FATAL_ERROR)

# project name and language
project(recipe-07 LANGUAGES C CXX)

# we default to Release build type
if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release CACHE STRING "Build type" FORCE)
endif()

message(STATUS "Build type: ${CMAKE_BUILD_TYPE}")

# -g
# /MDd /Zi /Ob0 /Od /RTC1
message(STATUS "C flags, Debug configuration: ${CMAKE_C_FLAGS_DEBUG}")
# -O3 -DNDEBUG
# /MD /O2 /Ob2 /DNDEBUG  /Ob2控制inline的函数展开的程度。 /MD Applications compiled with this option are statically linked to MSVCRT.lib. 
message(STATUS "C flags, Release configuration: ${CMAKE_C_FLAGS_RELEASE}")
# -O2 -DNDEBUG -g
message(STATUS "C flags, Release configuration with Debug info: ${CMAKE_C_FLAGS_RELWITHDEBINFO}")
# -Os -DNDEBUG
message(STATUS "C flags, minimal Release configuration: ${CMAKE_C_FLAGS_MINSIZEREL}")

message(STATUS "C++ flags, Debug configuration: ${CMAKE_CXX_FLAGS_DEBUG}")
message(STATUS "C++ flags, Release configuration: ${CMAKE_CXX_FLAGS_RELEASE}")
message(STATUS "C++ flags, Release configuration with Debug info: ${CMAKE_CXX_FLAGS_RELWITHDEBINFO}")
message(STATUS "C++ flags, minimal Release configuration: ${CMAKE_CXX_FLAGS_MINSIZEREL}")
