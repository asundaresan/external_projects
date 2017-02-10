cmake_minimum_required( VERSION 3.0 )

project( app CXX C )

include( ExternalProject )
ExternalProject_Add( THING
  URL ${CMAKE_CURRENT_SOURCE_DIR}/external/thing
  PREFIX ${CMAKE_CURRENT_BINARY_DIR}/tmp/thing
  INSTALL_DIR ${CMAKE_CURRENT_BINARY_DIR}/external/thing
  )
ExternalProject_Get_Property( THING install_dir )

add_library( thing STATIC IMPORTED )
set_property( TARGET thing PROPERTY IMPORTED_LOCATION ${install_dir}/lib/libthing.a)
add_dependencies( thing THING )


set( THING_INCLUDE_DIRS ${install_dir}/include )
message( STATUS "install_dir:${install_dir}" )

include_directories( ${THING_INCLUDE_DIRS} )

add_executable( myapp src/myapp.cpp )
target_link_libraries( myapp thing )



