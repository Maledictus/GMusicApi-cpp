cmake_minimum_required(VERSION 2.8.8)

project (gmusicapi-cpp)

if (UNIX OR (WIN32 AND MINGW))
	set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fvisibility=hidden -std=c++0x")

	if (NOT APPLE)
		set (CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} -Wl,--as-needed")
		set (CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -Wl,--as-needed")
	endif ()

	if (EXTRA_WARNINGS)
		set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra")
	endif ()
endif ()

find_package (Boost)

include_directories (${Boost_INCLUDE_DIRS}
	${CMAKE_CURRENT_BINARY_DIR}
	${CMAKE_CURRENT_SOURCE_DIR}
	..)

set (SRCS
	)
	
add_library (gmusicapi-cpp SHARED
	${SRCS}
	)

set_property (TARGET gmusicapi-cpp PROPERTY SOVERSION 0.0.1)
