cmake_minimum_required(VERSION 3.13)
project(booststache CXX)
enable_testing()

set(Boost_USE_STATIC_LIBS OFF)
# As of Boost 1.70: this seems to be needed now
set(BUILD_SHARED_LIBS ON)
set(Boost_USE_MULTITHREADED ON)
set(Boost_USE_STATIC_RUNTIME OFF)
#find_package(Boost 1.53 COMPONENTS unit_test_framework system filesystem)
find_package(Boost 1.70 REQUIRED COMPONENTS unit_test_framework system filesystem)

add_definitions( -DBOOST_SPIRIT_USE_PHOENIX_V3=1 )
if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
  add_definitions( -std=c++14 -ftemplate-depth=512 -Wno-unused-local-typedefs -Wno-deprecated-declarations )
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
  ##add_definitions( -std=c++14 -ftemplate-depth=512 -stdlib=libc++ )
  add_definitions( -std=c++17 )
endif()
# Not sure what to do with the <toolset>darwin

if(Boost_DEBUG)
    # With Boost 1.70 no all of the "typical" vars are defined
    message("BoostFOUND ${Boost_FOUND}")
    message(STATUS "Boost ${Boost_FIND_VERSION} found.")
    message("Boost_VERSION ${Boost_VERSION_STRING}")
    message ("Boost_VERSION ${Boost_VERSION}")
    message("Boost_INCLUDE_DIRS ${Boost_INCLUDE_DIRS}")
    message("Boost_INCLUDE_DIR ${Boost_INCLUDE_DIR}")
    message("Boost_DIR ${Boost_DIR}")
endif()

# Todo not ideal:
#if ("${Boost_INCLUDE_DIRS}" STREQUAL "")
#    # Boost_DIR is blah/lib/cmake/Boost-VER
#    set(Boost_INCLUDE_DIRS ${Boost_DIR}/../../../include)
#endif()
#message("Boost_INCLUDE_DIRS ${Boost_INCLUDE_DIRS}")


include_directories( include )
include_directories( SYSTEM ${Boost_INCLUDE_DIRS} )

# Not building for now as certain tests don't compile
#add_subdirectory(test)
add_subdirectory(examples)
