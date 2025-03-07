cmake_minimum_required(VERSION 3.0)

project(livox_sdk2)

set(CMAKE_CXX_STANDARD 11)

message(STATUS "main project dir: " ${PROJECT_SOURCE_DIR})

if (CMAKE_CROSSCOMPILING)
	set(THREADS_PTHREAD_ARG
		"PLEASE_FILL_OUT-FAILED_TO_RUN"
		CACHE STRING "Result from TRY_RUN" FORCE)
endif()

if (UNIX)
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread")
endif(UNIX)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC")

add_subdirectory(sdk_core)
add_subdirectory(samples)

set(SDK_CMAKE_ROOT ${CMAKE_CURRENT_LIST_DIR}/cmake)

if(NOT ${CMAKE_SOURCE_DIR} STREQUAL ${CMAKE_CURRENT_SOURCE_DIR})
  set(livox_sdk2_DIR ${SDK_CMAKE_ROOT} PARENT_SCOPE)
endif()

configure_file(
  ${SDK_CMAKE_ROOT}/livox_sdk2Config.cmake.in
  ${SDK_CMAKE_ROOT}/livox_sdk2Config.cmake @ONLY
)
