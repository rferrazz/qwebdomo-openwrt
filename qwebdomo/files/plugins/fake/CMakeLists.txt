cmake_minimum_required(VERSION 2.8.9)
project(fake)

add_definitions(-DQT_PLUGIN)
add_definitions(-DQT_NO_DEBUG)
add_definitions(-DQT_SHARED)

add_library(fake SHARED QWFakeActuator.cpp QWFakeActuator.h )
target_link_libraries(fake qwebdomo)
target_link_libraries( fake ${CMAKE_FIND_ROOT_PATH}/usr/lib/libQt5Core.so.5.0.2 )
target_link_libraries( fake ${CMAKE_FIND_ROOT_PATH}/usr/lib/libQt5Network.so.5.0.2 )
target_link_libraries( fake ${CMAKE_FIND_ROOT_PATH}/usr/lib/libQt5Xml.so.5.0.2 )