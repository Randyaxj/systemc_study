# cmake 最低版本需求，可以认为此file 是 top的 CMakeLists
cmake_minimum_required(VERSION 3.13.2)

# 工程名称  project() shouldn't be empty
project(my_test)

# 设置C++ stadard
set(CMAKE_CXX_STANDARD 11)

# 添加SystemC源代码目录为子项目  
add_subdirectory(third_party/systemc)  

# 添加SystemC头文件的包含路径  
find_path(SYSTEMC_INCLUDE_DIR systemc.h  
    PATHS ${CMAKE_CURRENT_SOURCE_DIR}/third_party/systemc/src
    NO_DEFAULT_PATH
    REQUIRED)  
  
include_directories(${SYSTEMC_INCLUDE_DIR})
  
set(SYSTEMC_LIBRARY_DIR ${CMAKE_BINARY_DIR}) # 这通常是顶级构建目录  
set(SYSTEMC_LIBRARIES libsystemc.a) # 或者libsystemc.so，取决于你的系统和构建配置 


# 添加你的源代码文件  
add_executable(my_executable main.cpp)  
  
# 链接SystemC库到你的项目中  
link_directories(${SYSTEMC_LIBRARY_DIR})  
target_link_libraries(my_executable ${SYSTEMC_LIBRARIES})  
  

# 确保SystemC在构建你的项目之前被构建  
# add_dependencies(my_executable systemc_build)



# 设置SystemC库的路径  
# set(SYSTEMC_INCLUDE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/third_party/systemc/include")  
# set(SYSTEMC_LIBRARY_DIR "${CMAKE_CURRENT_SOURCE_DIR}/third_party/systemc/lib")  
  



