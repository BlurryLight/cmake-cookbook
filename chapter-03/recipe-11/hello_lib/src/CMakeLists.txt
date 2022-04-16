# project(hellolib VERSION 1.0.0)
aux_source_directory(. DIR_SRCS)
add_library(${PROJECT_NAME} SHARED ${DIR_SRCS})

# 当编译的时候，其include dir展开为${CMAKE_SOURCE_DIR}/include>
# 当install的时候，其include dir展开为<prefix>/include
target_include_directories(${PROJECT_NAME} PUBLIC
        $<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include>)

# ------------------------------- install script -------------------------------
# Prepare exposed headers
set(HEADERS ${CMAKE_SOURCE_DIR}/include/hello.h)
set_target_properties(${PROJECT_NAME} PROPERTIES PUBLIC_HEADER "${HEADERS}")

# TARGETS 编译后的产物
# FILES 其他依赖文件
# EXPORT 导出${ProjectName}Targets目标，这个目标的具体操作在后面定义
install(TARGETS ${PROJECT_NAME}
        EXPORT ${PROJECT_NAME}Targets
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
        RUNTIME DESTINATION bin
        PUBLIC_HEADER DESTINATION include)

# Generate library version info which will generate xxxConfigVersion.cmake,
# the ${PACKAGE_VERSION} is the version defined in project()
include(CMakePackageConfigHelpers)
# 根据VERSION信息生成${PROJECT_NAME}ConfigVersion.cmake文件
write_basic_package_version_file(
        ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}ConfigVersion.cmake
        VERSION ${PACKAGE_VERSION}
        COMPATIBILITY SameMajorVersion)

# 导出{PROJECT_NAME}Targets这个目标的具体动作是把${PROJECT_NAME}Targets.cmake文件写到对应的目录
# 会自动生成${PROJECT_NAME}Targets.cmake并包含相关的目标
install(EXPORT ${PROJECT_NAME}Targets
        FILE ${PROJECT_NAME}Targets.cmake
        DESTINATION "lib/cmake/${PROJECT_NAME}")

    # 根据模版生成config文件，该模版文件主要是为了添加第三方依赖(find_dependency)
configure_package_config_file(
        cmake/Config.cmake.in ${PROJECT_NAME}Config.cmake
        INSTALL_DESTINATION "lib/cmake/${PROJECT_NAME}")

# 把version和config都写到对应的目录
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake
        ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}ConfigVersion.cmake
        DESTINATION "lib/cmake/${PROJECT_NAME}")
