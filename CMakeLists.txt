cmake_minimum_required(VERSION 2.8)
project(Critters)

# Set up SFML
set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/CMake/Modules" ${CMAKE_MODULE_PATH})
find_package(SFML 2 COMPONENTS system window audio REQUIRED)
include_directories(${SFML_INCLUDE_DIR})

# Set up OpenGL
find_package(OpenGL REQUIRED)
include_directories(${OPENGL_INCLUDE_DIR})

# Set up GLEW
find_package(GLEW REQUIRED)
include_directories(${GLEW_INCLUDE_DIRS})

# Add additional flags to gcc and clang
if (CMAKE_COMPILER_IS_GNUCXX OR CMAKE_COMPILER_IS_CLANGXX OR "${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
    add_definitions("-std=c++11 -pedantic -Wall -Wextra")
endif ()

# src globbing
FILE(GLOB Sources src/*.cpp)
FILE(GLOB Headers src/*.hpp)

add_executable(critters ${Sources} ${Headers} 
src/Utilities/Program.hpp src/Utilities/Program.cpp
src/Utilities/Shader.hpp src/Utilities/Shader.cpp)

target_link_libraries(critters ${SFML_LIBRARIES} ${OPENGL_LIBRARIES} ${GLEW_LIBRARIES})
