cmake_minimum_required(VERSION 3.5.1)

project(SDL2Test)

include(ExternalProject)
set(EXTERNAL_INSTALL_LOCATION ${CMAKE_BINARY_DIR}/external)

ExternalProject_Add(
	SDLlib
	GIT_REPOSITORY "https://github.com/SDL-mirror/SDL.git"
	CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${EXTERNAL_INSTALL_LOCATION}
)

ExternalProject_Add(
    SDLimage
    GIT_REPOSITORY "https://github.com/SDL-mirror/SDL_image.git"
    CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${EXTERNAL_INSTALL_LOCATION}
	add_custom_command(COMMAND make)
)

include_directories(${EXTERMAL_INSTALL_LOCATION}/include)
link_directories(${EXTERNAL_INSTALL_LOCATION}/lib)

add_executable(SDL2Test SDLimage Main.cpp)
add_dependencies(SDL2Test SDLlib SDLimage) 
#target_link_libraries(SDL2Test SDLlib)
