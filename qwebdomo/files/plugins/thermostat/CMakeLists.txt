cmake_minimum_required(VERSION 2.8.9)
project(GME-thermostat)

add_definitions(-DQT_PLUGIN)
add_definitions(-DQT_NO_DEBUG)
add_definitions(-DQT_SHARED)

add_library( GME-thermostat SHARED thermostatactuator.cpp thermostatactuator.h )
target_link_libraries(GME-thermostat qwebdomo)
target_link_libraries(GME-thermostat ${CMAKE_FIND_ROOT_PATH}/usr/lib/libqtserialport.so.5.1)
target_link_libraries( whia ${CMAKE_FIND_ROOT_PATH}/usr/lib/libQt5Core.so.5.0.2 )
target_link_libraries( whia ${CMAKE_FIND_ROOT_PATH}/usr/lib/libQt5Network.so.5.0.2 )
target_link_libraries( whia ${CMAKE_FIND_ROOT_PATH}/usr/lib/libQt5Xml.so.5.0.2 )

