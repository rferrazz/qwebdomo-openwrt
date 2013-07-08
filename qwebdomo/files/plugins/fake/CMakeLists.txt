cmake_minimum_required(VERSION 2.8.9)
project(fake)

add_definitions(${Qt5Core_DEFINITIONS} ${Qt5Network_DEFINITIONS} ${Qt5Xml_DEFINITIONS})
add_definitions(-DQT_PLUGIN)
add_definitions(-DQT_SHARED)
add_definitions(-DQT_DLL)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${Qt5Core_EXECUTABLE_COMPILE_FLAGS} ${Qt5Network_EXECUTABLE_COMPILE_FLAGS} ${Qt5Xml_EXECUTABLE_COMPILE_FLAGS}")

add_library(fake SHARED QWFakeActuator.cpp QWFakeActuator.h )
target_link_libraries(fake qwebdomo)
target_link_libraries( fake ${CMAKE_FIND_ROOT_PATH}/usr/lib/libQt5Core.so.5.0.2 )
target_link_libraries( fake ${CMAKE_FIND_ROOT_PATH}/usr/lib/libQt5Network.so.5.0.2 )
target_link_libraries( fake ${CMAKE_FIND_ROOT_PATH}/usr/lib/libQt5Xml.so.5.0.2 )

qt5_use_modules(${PROJECT_NAME} Core)
qt5_use_modules(${PROJECT_NAME} Network)
qt5_use_modules(${PROJECT_NAME} Xml)