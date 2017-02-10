cmake_minimum_required( VERSION 3.0 )

project( app CXX C )

include( ExternalProject )
ExternalProject_Add(THING
  SOURCE_DIR ${CMAKE_SOURCE_DIR}/external/thing
  INSTALL_DIR ${CMAKE_BINARY_DIR}/external/thing
  DOWNLOAD_COMMAND ""
  UPDATE_COMMAND ""
  CMAKE_ARGS "-DCMAKE_INSTALL_PREFIX=${CMAKE_BINARY_DIR}/external/thing"
    #    -DCMAKE_CXX_FLAGS=${CMAKE_CXX_FLAGS} 
    #    -DCMAKE_C_FLAGS=${CMAKE_C_FLAGS} 
    #    -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
    #    ${USE_PROJECT_CMAKE_MODULE_PATH}
    #INSTALL_COMMAND ""
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



