project (QtDBMigration)
cmake_minimum_required(VERSION 2.8.11)

find_package(Qt5Core QUIET)
find_package(Qt5Sql QUIET)

set(QTCORE_LIBRARIES ${Qt5Core_LIBRARIES})
# if there is no QT_ROOT, try to deduce it from Qt QtCore include
if ("${QT_ROOT}" STREQUAL "")
    set(QT_ROOT ${QT_QTCORE_INCLUDE_DIR}/../..)
endif()
include_directories(${Qt5Core_INCLUDE_DIRS})
include_directories(${Qt5Sql_INCLUDE_DIRS})

macro(qt_wrap_cpp)
    qt5_wrap_cpp(${ARGN})
endmacro()

# All build libraries are moved to this directory
SET(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR})

set(LIB_SUFFIX "" CACHE STRING "Define suffix of directory name (32/64)")
set(LIB_DESTINATION "${CMAKE_INSTALL_PREFIX}/lib${LIB_SUFFIX}" CACHE STRING "Library directory name" FORCE)

add_subdirectory(src)
