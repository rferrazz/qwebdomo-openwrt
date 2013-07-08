cmake_minimum_required(VERSION 2.8.9)
project(qwebdomo)

# Tell CMake to run moc when necessary:
set(CMAKE_AUTOMOC ON)
# As moc files are generated in the binary dir, tell CMake
# to always look for includes there:
set(CMAKE_INCLUDE_CURRENT_DIR ON)

find_package ( Qt5Core REQUIRED)
find_package ( Qt5Network REQUIRED)
find_package ( Qt5Xml REQUIRED)

include_directories("./core"
                    "./core/device"
                    "./whia"
                    "./plugins"
                    "./plugins/GME-thermostat"
                    "./plugins/fake"
                    ${CMAKE_CURRENT_BINARY_DIR} )

include_directories(${CMAKE_FIND_ROOT_PATH}/usr/include/QtXml 
                    ${CMAKE_FIND_ROOT_PATH}/usr/include/QtCore 
                    ${CMAKE_FIND_ROOT_PATH}/usr/include/QtNetwork
                    ${CMAKE_FIND_ROOT_PATH}/usr/include/qxmpp
                    ${CMAKE_FIND_ROOT_PATH}/usr/include/QtSerialPort
                    ${CMAKE_FIND_ROOT_PATH}/usr/include )
                    
add_definitions(${Qt5Core_DEFINITIONS} ${Qt5Network_DEFINITIONS} ${Qt5Xml_DEFINITIONS})

#webdomo constants
set(QW_VERSION_MAJOR "0")
set(QW_VERSION_MINOR "5")
set(QW_VERSION "${QW_VERSION_MAJOR}.${QW_VERSION_MINOR}")
add_definitions(-DQT_DEBUG=1)
add_definitions(-DPLUGINS_PATH="/usr/lib/webdomo/plugins")
add_definitions(-DCONF_PATH="/etc/whia")
add_definitions(-DQW_VERSION_MAJOR=${QW_VERSION_MAJOR})
add_definitions(-DQW_VERSION_MINOR=${QW_VERSION_MINOR})
add_definitions(-DQ_VERSION=${QW_VERSION})

MESSAGE ( ${CMAKE_CXX_FLAGS} ${Qt5Core_EXECUTABLE_COMPILE_FLAGS} )

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${Qt5Core_EXECUTABLE_COMPILE_FLAGS} ${Qt5Network_EXECUTABLE_COMPILE_FLAGS} ${Qt5Xml_EXECUTABLE_COMPILE_FLAGS}")

file( GLOB qwebdomo_core_src "./core/*.cpp" )
file( GLOB qwebdomo_device_src "./core/device/*.cpp" )
set( qwebdomo_src ${qwebdomo_core_src} ${qwebdomo_device_src} )

file( GLOB whia "./whia/*.cpp" )
set( whia_src ${whia} )

add_library( qwebdomo SHARED ${qwebdomo_src} )
set_target_properties( qwebdomo PROPERTIES VERSION ${QW_VERSION})
target_link_libraries( qwebdomo ${CMAKE_FIND_ROOT_PATH}/usr/lib/libQt5Core.so.5.0.2 )
target_link_libraries( qwebdomo ${CMAKE_FIND_ROOT_PATH}/usr/lib/libQt5Network.so.5.0.2 )
target_link_libraries( qwebdomo ${CMAKE_FIND_ROOT_PATH}/usr/lib/libqxmpp.so )

add_executable( whia ${whia_src} )
target_link_libraries( whia ${CMAKE_FIND_ROOT_PATH}/usr/lib/libQt5Core.so.5.0.2 )
target_link_libraries( whia ${CMAKE_FIND_ROOT_PATH}/usr/lib/libQt5Network.so.5.0.2 )
target_link_libraries( whia ${CMAKE_FIND_ROOT_PATH}/usr/lib/libQt5Xml.so.5.0.2 )
target_link_libraries( whia qwebdomo)

add_definitions(-DQT_PLUGIN)
add_library(fake SHARED ./plugins/fake/QWFakeActuator.cpp )
target_link_libraries(fake qwebdomo)

add_library( GME-thermostat SHARED ./plugins/GME-thermostat/thermostatactuator.cpp )
target_link_libraries(GME-thermostat qwebdomo)
target_link_libraries(GME-thermostat ${CMAKE_FIND_ROOT_PATH}/usr/lib/libqtserialport.so.5.1)

