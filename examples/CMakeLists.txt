foreach( EXAMPLE example1 example2 example3 )
  add_executable( ${EXAMPLE} ${EXAMPLE}.cpp )
  target_link_libraries (${EXAMPLE} Boost::system)
  # Don't really need Boost::system to link against;
  # However, need a Boost library so the search path to BOOST_ROOT/include will be added
endforeach()


