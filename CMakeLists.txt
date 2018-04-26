cmake_minimum_required(VERSION 3.5.1)

project(SDL2Test)

include(ExternalProject)
include_directories(${CMAKE_SOURCE_DIR}/external/SDL/include ${CMAKE_SOURCE_DIR}/external/SDL_image)

ExternalProject_Add(
  SDLlib
  SOURCE_DIR ${CMAKE_SOURCE_DIR}/external/SDL
  CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${CMAKE_SOURCE_DIR}/build -DCMAKE_BUILD_TYPE=Release
)

ExternalProject_Add(
  SDLimage
  DEPENDS SDLlib
  SOURCE_DIR ${CMAKE_SOURCE_DIR}/external/SDL_image
  CONFIGURE_COMMAND ""
  BUILD_COMMAND "msbuild.exe ${CMAKE_SOURCE_DIR}/SDL_image/VisualC/SDL_image.sln /t:Build /p:Configuration=Release;Platform=Win32"
)

add_executable(SDL2Test Main.cpp)
add_dependencies(SDL2Test SDLlib SDLimage)

if (WIN32)
	target_link_libraries(SDL2Test ${CMAKE_SOURCE_DIR}/build/lib/SDL2.lib ${CMAKE_SOURCE_DIR}/build/lib/SDL2main.lib)
endif()