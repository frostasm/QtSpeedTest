cmake_minimum_required(VERSION 3.14)

project(qtspeedtest VERSION 1.0.0 LANGUAGES CXX)

option(DISABLE_COMPILER_WARNINGS "Disable compiler warnings" OFF)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(QT NAMES Qt6 Qt5 REQUIRED COMPONENTS Core Network Xml)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Core Network Xml)

add_library(${PROJECT_NAME} SHARED
    QtSpeedTest
    libqspeedtest_global.h
    speedtest.cpp
    speedtest.h
    speedtest.pro
    speedtest_p.h
    stclient.cpp
    stclient.h
    stconfigclient.cpp
    stconfigclient.h
    stconfigdownload.cpp
    stconfigdownload.h
    stconfigdownloadsocket.cpp
    stconfigdownloadsocket.h
    stconfigglobal.cpp
    stconfigglobal.h
    stconfiglatency.cpp
    stconfiglatency.h
    stconfigupload.cpp
    stconfigupload.h
    stconfiguploadsocket.cpp
    stconfiguploadsocket.h
    stdownloader.cpp
    stdownloader.h
    stdummybuffer.cpp
    stdummybuffer.h
    stserveritem.cpp
    stserveritem.h
    stserverlist.cpp
    stserverlist.h
    stserversorter.cpp
    stserversorter.h
    stuploader.cpp
    stuploader.h
    stuploaderhttp.cpp
    stuploaderhttp.h
)

target_link_libraries(${PROJECT_NAME} PRIVATE
    Qt${QT_VERSION_MAJOR}::Core
    Qt${QT_VERSION_MAJOR}::Network
    Qt${QT_VERSION_MAJOR}::Xml
)

set_target_properties(${PROJECT_NAME} PROPERTIES
    VERSION ${PROJECT_VERSION}
    SOVERSION 1
 )

target_compile_definitions(${PROJECT_NAME} PRIVATE LIBQSPEEDTEST_LIBRARY)
target_include_directories(${PROJECT_NAME} PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")
add_library(qtspeedtest::static ALIAS qtspeedtest)

if (DISABLE_COMPILER_WARNINGS)
    if ( CMAKE_COMPILER_IS_GNUCXX )
        target_compile_options(${PROJECT_NAME} PRIVATE -w)
    endif()
    if ( MSVC )
        target_compile_options(${PROJECT_NAME} PRIVATE /w)
    endif()
endif()

