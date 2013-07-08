cmake_minimum_required(VERSION 2.8.9)
project(qtserialport)

# Tell CMake to run moc when necessary:
set(CMAKE_AUTOMOC ON)
# As moc files are generated in the binary dir, tell CMake
# to always look for includes there:
set(CMAKE_INCLUDE_CURRENT_DIR ON)

find_package ( Qt5Core REQUIRED)

include_directories( "./src/serialport"
                     "./src"
                     ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/usr/include
                     ${CMAKE_CURRENT_BINARY_DIR} )

include_directories( ${CMAKE_FIND_ROOT_PATH}/usr/include/QtCore ${CMAKE_FIND_ROOT_PATH}/usr/include/QtCore/5.0.2/QtCore ${Qt5Core_INCLUDE_DIRS} )
add_definitions( ${Qt5Core_DEFINITIONS} )
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${Qt5Core_EXECUTABLE_COMPILE_FLAGS}" )

set( src ./src/serialport/qserialport.cpp
         ./src/serialport/qserialport_unix.cpp
         ./src/serialport/qserialportinfo.cpp
         ./src/serialport/qserialportinfo_unix.cpp
         ./src/serialport/qttylocker_unix.cpp
         )

set( headers ./src/serialport/qserialport.h 
             ./src/serialport/qserialport_p.h 
             ./src/serialport/qserialport_unix_p.h 
             ./src/serialport/qserialportinfo.h
             ./src/serialport/qserialportinfo_p.h
             ./src/serialport/qttylocker_unix_p.h )
         
add_library( qtserialport SHARED ${src} )
set_target_properties( qtserialport PROPERTIES VERSION "5.1" )

target_link_libraries( qtserialport ${CMAKE_FIND_ROOT_PATH}/usr/lib/libQt5Core.so.5.0.2)