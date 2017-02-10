cmake_minimum_required( VERSION 3.0 )

project( thing CXX C )

include_directories( include )
add_library( thing src/thing.cpp )

install( TARGETS thing DESTINATION ${CMAKE_INSTALL_DIR}/lib )
install( FILES include/thing.h DESTINATION ${CMAKE_INSTALL_DIR}/include )
