cmake_minimum_required(VERSION 3.10)

#-------------------------------------------------------------------------------
# BOOTSTRAP w/ latest bootstrap/cmake scripts
#-------------------------------------------------------------------------------
include(FetchContent)
FetchContent_Declare(cmake
  GIT_REPOSITORY git@github.com:jiverson002/bootstrap-cmake.git
)
FetchContent_MakeAvailable(cmake)

#-------------------------------------------------------------------------------
# Import dependencies (needed to ensure that target efika is known)
#-------------------------------------------------------------------------------
set(core_GIT_REPOSITORY git@github.com/jiverson002/efika-core.git)

import(core)

#-------------------------------------------------------------------------------
# SUBPROJECT configuration
#-------------------------------------------------------------------------------
project(${BS_PROJECT_NAME}-data LANGUAGES NONE)

cmake_policy(SET CMP0079 NEW)

#-------------------------------------------------------------------------------
# LIBRARY configuration
#-------------------------------------------------------------------------------
add_library(${PROJECT_NAME} INTERFACE)

target_include_directories(${PROJECT_NAME} INTERFACE
  $<BUILD_INTERFACE:${PROJECT_BINARY_DIR}/include>
)

target_link_libraries(${BS_PROJECT_NAME} INTERFACE ${PROJECT_NAME})

#-------------------------------------------------------------------------------
# Set data path
#-------------------------------------------------------------------------------
set(EFIKA_DATA_PATH ${PROJECT_SOURCE_DIR})

configure_file(include/efika/data/path.h.in include/efika/data/path.h @ONLY)
