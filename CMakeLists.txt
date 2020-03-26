cmake_minimum_required( VERSION 3.10 )

# Subproject of efika
project( efika-data LANGUAGES NONE )

#-------------------------------------------------------------------------------
# COMPONENT configuration
#-------------------------------------------------------------------------------
add_library( ${PROJECT_NAME} INTERFACE )

target_include_directories( ${PROJECT_NAME}
  INTERFACE $<BUILD_INTERFACE:${PROJECT_BINARY_DIR}/include> )

add_library( Efika::data ALIAS ${PROJECT_NAME} )

#-------------------------------------------------------------------------------
# Set data path
#-------------------------------------------------------------------------------
set(EFIKA_DATA_PATH ${PROJECT_SOURCE_DIR})

configure_file(include/efika/data.h.in include/efika/data.h @ONLY)
