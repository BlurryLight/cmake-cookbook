# set minimum cmake version
cmake_minimum_required(VERSION 3.10 FATAL_ERROR)

# project name and language
project(recipe-05 LANGUAGES CXX)

# define executable
add_executable(processor-info "")

# and its source file
target_sources(processor-info
  PRIVATE
    processor-info.cpp
  )

# and its include directories
target_include_directories(processor-info
  PRIVATE
  # the config.h will be generated there
    ${PROJECT_BINARY_DIR}
  )

foreach(key
  IN ITEMS
    NUMBER_OF_LOGICAL_CORES
    NUMBER_OF_PHYSICAL_CORES
    TOTAL_VIRTUAL_MEMORY
    AVAILABLE_VIRTUAL_MEMORY
    TOTAL_PHYSICAL_MEMORY
    AVAILABLE_PHYSICAL_MEMORY
    IS_64BIT
    HAS_FPU
    HAS_MMX
    HAS_MMX_PLUS
    HAS_SSE
    HAS_SSE2
    HAS_SSE_FP
    HAS_SSE_MMX
    HAS_AMD_3DNOW
    HAS_AMD_3DNOW_PLUS
    HAS_IA64
    OS_NAME
    OS_RELEASE
    OS_VERSION
    OS_PLATFORM
  )
  # 把查询到的结果存到_HAS_SSE_里
  # 下一行的configure_file 会从cache里查_HAS_SSE_这个值
  cmake_host_system_information(RESULT _${key} QUERY ${key})
endforeach()

# 常用的flags
# COPYONLY Copy the file without replacing any variable references or other content. This option may not be used with NEWLINE_STYLE.
# @ONLY 只替换@包围的变量，而不替换${}这样的变量
# 推荐使用#cmakedefine 如果值被定义了，就会变成define，如果没有就会被注释掉，避免空值宏
configure_file(config.h.in config.h @ONLY)
