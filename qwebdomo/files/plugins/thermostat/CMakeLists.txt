cmake_minimum_required(VERSION 2.8.9)
project(GME-thermostat)

add_definitions(-DQT_PLUGIN)
add_definitions(-DQT_SHARED)
add_definitions(-DQT_DLL)
add_definitions(${Qt5Core_DEFINITIONS} ${Qt5Network_DEFINITIONS} ${Qt5Xml_DEFINITIONS})

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${Qt5Core_EXECUTABLE_COMPILE_FLAGS} ${Qt5Network_EXECUTABLE_COMPILE_FLAGS} ${Qt5Xml_EXECUTABLE_COMPILE_FLAGS}")

add_library( GME-thermostat SHARED thermostatactuator.cpp thermostatactuator.h )
target_link_libraries(GME-thermostat qwebdomo)
target_link_libraries(GME-thermostat ${CMAKE_FIND_ROOT_PATH}/usr/lib/libqtserialport.so.5.1)
target_link_libraries( GME-thermostat ${CMAKE_FIND_ROOT_PATH}/usr/lib/libQt5Core.so.5.0.2 )
target_link_libraries( GME-thermostat ${CMAKE_FIND_ROOT_PATH}/usr/lib/libQt5Network.so.5.0.2 )
target_link_libraries( GME-thermostat ${CMAKE_FIND_ROOT_PATH}/usr/lib/libQt5Xml.so.5.0.2 )

