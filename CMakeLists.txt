cmake_minimum_required(VERSION 3.5.1)

project(SDL2Test)

include(ExternalProject)
ExternalProject_Add(
	SDLlib
	GIT_REPOSITORY "https://github.com/SDL-mirror/SDL.git"
	SOURCE_DIR ${CMAKE_SOURCE_DIR}
)
ExternalProject_Get_Property(INCLUDE_DIR ${SOURCE_DIR}/include)
include_directories(${INCLUDE_DIR})

add_executable(SDL2Test Main.cpp)