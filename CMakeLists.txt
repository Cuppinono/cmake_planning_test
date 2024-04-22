cmake_minimum_required(VERSION 3.29.0)
project(zcc_test_planning)
set(CMAKE_CXX_STANDARD 17)

#变量和目录设置
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin) # Windows 动态库和exe都指定到bin目录下面
# CMAKE_LIBRARY_OUTPUT_DIRECTORY   #Linux 动态库和可执行文件
# CMAKE_ARCHIVE_OUTPUT_DIRECTORY   #静态库 ，而不会去管可执行文件

#动态库和依赖的头文件目录
aux_source_directory(${PROJECT_SOURCE_DIR}/src SRC_LISTS)
add_library(common
SHARED
${SRC_LISTS}
)
target_include_directories(common
PUBLIC 
${PROJECT_SOURCE_DIR}/include
)

#可执行文件和依赖的头文件目录
add_executable(planning_main planning_main.cpp)
target_include_directories(planning_main
PUBLIC
${PROJECT_SOURCE_DIR}/include
)

#链接 让可执行文件链接动态库
target_link_libraries(planning_main
PUBLIC
common
)