# 这个指令会把当前CMakeLists.txt所在的目录加到当前CMakeLists.txt的targets的interface属性上，
# 任何引用了这个target的target都会间接引入当前目录
set(CMAKE_INCLUDE_CURRENT_DIR_IN_INTERFACE ON)

add_library(sum_integers sum_integers.cpp)

add_executable(sum_up main.cpp)

target_link_libraries(sum_up sum_integers)
