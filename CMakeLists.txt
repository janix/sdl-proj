cmake_minimum_required(VERSION 3.5.1)

project(SDL2Test)

include(ExternalProject)
ExternalProject_Add(
	SDLlib
	GIT_REPOSITORY "https://github.com/SDL-mirror/SDL.git"
	SOURCE_DIR ${CMAKE_SOURCE_DIR}/src
)
ExternalProject_Get_Property(SDLlib ${PREFIX}/include)
include_directories(${PREFIX}/include)

add_executable(SDL2Test Main.cpp)