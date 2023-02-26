cmake_minimum_required(VERSION 3.6)

project(MY_APP)

#这里添加了头文件查找目录
include_directories(${CMAKE_SOURCE_DIR}/SDL/include)

#生成main.so 需要引用SDL2.so库 （SDL2.so是脚本文件jni/SDL/CMakeLists.txt 生成的）
find_library(SDL2 SDL2)

add_library(main SHARED)

#添加这个main.so 的原文件，把 SDL2Android.c 放到这个so库中（SDL_android_main.c 是自带的一个空文件，其他也可以直接使用这个文件）
target_sources(main PRIVATE ${CMAKE_SOURCE_DIR}/SDL/src/main/android/SDL_android_main.c
        ${CMAKE_SOURCE_DIR}/SDL/src/SDL2Android.c)

#把SDL2.so 加入main.so 中
target_link_libraries(main SDL2)
