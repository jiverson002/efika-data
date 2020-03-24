cmake_minimum_required(VERSION 3.13)

#-------------------------------------------------------------------------------
# BOOTSTRAP
#-------------------------------------------------------------------------------
include(${CMAKE_CURRENT_LIST_DIR}/cmake/Bootstrap.cmake)

#-------------------------------------------------------------------------------
# SUBPROJECT configuration
#-------------------------------------------------------------------------------
project(${BS_PROJECT_NAME}-data LANGUAGES NONE)

cmake_policy(SET CMP0079 NEW)

#-------------------------------------------------------------------------------
# LIBRARY configuration
#-------------------------------------------------------------------------------
add_library(${PROJECT_NAME} INTERFACE)

target_link_libraries(${BS_PROJECT_NAME} INTERFACE ${PROJECT_NAME})

target_include_directories(${PROJECT_NAME} INTERFACE
  $<BUILD_INTERFACE:${PROJECT_BINARY_DIR}/include>
)

#-------------------------------------------------------------------------------
# Set data path
#-------------------------------------------------------------------------------
set(EFIKA_DATA_PATH ${PROJECT_SOURCE_DIR})

configure_file(include/efika/data.h.in include/efika/data.h @ONLY)
