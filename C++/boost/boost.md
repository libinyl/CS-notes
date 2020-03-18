## 链接选项

-lboost_program_options

https://blog.csdn.net/Windgs_YF/article/details/81201456

## 查看版本

boost/version.hpp

## boost 与 clion

头文件位于 /usr/local/include/boost
库路径位于 /usr/local/lib

## cmake


```
//https://stackoverflow.com/a/28762275
cmake_minimum_required(VERSION 3.10)
project(untitled69)

set(CMAKE_CXX_STANDARD 11)

set(Boost_USE_STATIC_LIBS        ON) # only find static libs
set(Boost_USE_MULTITHREADED      ON)
set(Boost_USE_STATIC_RUNTIME    OFF)
find_package(Boost 1.70.0 COMPONENTS date_time filesystem system)
if(Boost_FOUND)
    include_directories(${Boost_INCLUDE_DIRS})
    add_executable(untitled69 main.cpp)
    target_link_libraries(untitled69 ${Boost_LIBRARIES})
endif()


```
