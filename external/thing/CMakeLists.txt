cmake_minimum_required( VERSION 3.0 )

project( thing CXX C )

include_directories( include )
add_library( thing src/thing.cpp )

install( TARGETS thing DESTINATION lib )
install( DIRECTORY include/thing DESTINATION include )
