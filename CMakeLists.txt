cmake_minimum_required(VERSION 3.5.1)

project(SDL2Test)

include(ExternalProject)
include_directories(external/SDL/include external/SDL_image)

ExternalProject_Add(
  SDLlib
  SOURCE_DIR "${CMAKE_SOURCE_DIR}/external/SDL"
  CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${CMAKE_BINARY_DIR}

)

add_executable(SDL2Test Main.cpp)
add_dependencies(SDL2Test SDLlib)

target_link_libraries(SDL2Test ${CMAKE_BINARY_DIR}/lib/libSDL2.a)
