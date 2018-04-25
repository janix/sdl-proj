cmake_minimum_required(VERSION 3.5.1)

project(SDL2Test)

include_directories(external/SDL/include)
link_directories(external/lib)

add_executable(SDL2Test Main.cpp)
#add_dependencies(SDL2Test) 
#target_link_libraries(SDL2Test SDLlib)
