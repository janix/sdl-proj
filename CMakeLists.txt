cmake_minimum_required(VERSION 3.5.1)

project(SDL2Test)

include(ExternalProject)
include_directories(${CMAKE_SOURCE_DIR}/external/SDL/include ${CMAKE_SOURCE_DIR}/external/SDL_image)

if(WIN32)
	ExternalProject_Add(
  		SDLlib
  		SOURCE_DIR ${CMAKE_SOURCE_DIR}/external/SDL
  		CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${CMAKE_SOURCE_DIR}/build -DCMAKE_BUILD_TYPE=Release
	)
elseif(UNIX)
	ExternalProject_Add(
  		SDLlib
  		SOURCE_DIR ${CMAKE_SOURCE_DIR}/external/SDL
  		CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${CMAKE_SOURCE_DIR}/build -DCMAKE_BUILD_TYPE=Release
	)
endif()

#set(ENV{PATH} "${CMAKE_SOURCE_DIR}/build/bin")


if(WIN32)

	ExternalProject_Add(
  		SDLimage
#  		DEPENDS SDLlib
  		SOURCE_DIR ${CMAKE_SOURCE_DIR}/external/SDL_image
  		CONFIGURE_COMMAND ""
  		BUILD_COMMAND "msbuild.exe ${CMAKE_SOURCE_DIR}/SDL_image/VisualC/SDL_image.sln /t:Build /p:Configuration=Release;Platform=Win32"
	)
elseif(UNIX)
	ExternalProject_Add(
		SDLimage
#		DEPENDS SDLlib
		SOURCE_DIR ${CMAKE_SOURCE_DIR}/external/SDL_image
		CONFIGURE_COMMAND "${CMAKE_SOURCE_DIR}/external/SDL_image/configure" # --prefix=${CMAKE_SOURCE_DIR}/build/bin"
		BUILD_COMMAND "make all"
#		INSTALL_COMMAND "make install"
)
endif()

add_executable(SDL2Test Main.cpp)
add_dependencies(SDL2Test SDLlib SDLimage)
#add_dependencies(SDL2Test SDLimage)

if (WIN32)
	target_link_libraries(SDL2Test ${CMAKE_SOURCE_DIR}/build/lib/SDL2.lib ${CMAKE_SOURCE_DIR}/build/lib/SDL2main.lib)
elseif(UNIX)
	target_link_libraries(SDL2Test ${CMAKE_SOURCE_DIR}/build/lib/libSDL2.a ${CMAKE_SOURCE_DIR}/build/lib/libSDL2main.a)
endif()
