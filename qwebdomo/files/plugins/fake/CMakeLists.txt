cmake_minimum_required(VERSION 2.8.9)
project(fake)

add_definitions(-DQT_PLUGIN)
add_definitions(-DQT_NO_DEBUG)
add_definitions(-DQT_SHARED)

add_library(fake SHARED QWFakeActuator.cpp QWFakeActuator.h )
target_link_libraries(fake qwebdomo)