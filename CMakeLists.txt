cmake_minimum_required(VERSION 3.2)

# arcd target (required)
set(HEADERS_DIR ${CMAKE_CURRENT_SOURCE_DIR})
set(HEADERS arcd.h)
set(SOURCES arcd.c)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c99 -Wall -Wextra -Werror -pedantic-errors")

add_library(arcd ${HEADERS} ${SOURCES})
target_include_directories(arcd PUBLIC $<BUILD_INTERFACE:${HEADERS_DIR}>)

# install (optional)
if(ARCD_CONFIGURE_INSTALL)
	if(NOT DEFINED INSTALL_INCLUDE_DIR)
		set(INSTALL_INCLUDE_DIR include)
	endif()
	if(NOT DEFINED INSTALL_LIB_DIR)
		set(INSTALL_LIB_DIR lib)
	endif()
	install(TARGETS arcd EXPORT arcd
		INCLUDES DESTINATION ${INSTALL_INCLUDE_DIR}
		ARCHIVE DESTINATION ${INSTALL_LIB_DIR})
	install(DIRECTORY ${HEADERS_DIR}
		DESTINATION ${INSTALL_INCLUDE_DIR}
		FILES_MATCHING PATTERN "*.h")
endif()


set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c99 -Wall -Wextra -Werror -pedantic-errors")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall -Wextra -Werror -pedantic-errors")

add_library(adaptive_model adaptive_model.c adaptive_model.h)
target_include_directories(adaptive_model PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>)
target_link_libraries(adaptive_model arcd)

add_executable(arcd_stream arcd_stream.c)
target_link_libraries(arcd_stream arcd adaptive_model)
