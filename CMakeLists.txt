cmake_minimum_required(VERSION 3.20 FATAL_ERROR)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

project(cs200-assignment-5 VERSION 0.1)

set(CMAKE_CXX_STANDARD_INCLUDE_DIRECTORIES ${CMAKE_CXX_IMPLICIT_INCLUDE_DIRECTORIES})


find_package(OpenGL REQUIRED)
find_package(glm REQUIRED)
find_package(SDL2 REQUIRED CONFIG REQUIRED COMPONENTS SDL2)
find_package(GLEW REQUIRED)

add_compile_options(-fdiagnostics-color=always)
add_compile_options(-Wextra -Wall -Wpedantic -std=c++11)

add_library(Affine src/Affine.cpp)
target_link_libraries(Affine PRIVATE glm::glm)

add_library(SquareMesh src/SquareMesh.cpp)
target_link_libraries(SquareMesh PRIVATE glm::glm)

add_library(SolidRender src/SolidRender.cpp)
target_link_libraries(SolidRender PRIVATE glm::glm)

add_library(Camera src/Camera.cpp)
target_link_libraries(Camera PRIVATE glm::glm)

add_executable(CameraTest src/CameraTest.cpp)
target_link_libraries(CameraTest PRIVATE Camera SquareMesh SolidRender Affine OpenGL glm::glm SDL2::SDL2 ${GLEW_LIBRARIES})
include_directories(CameraTest ${GLEW_INCLUDE_DIRS})

# Linking all to test driver
add_executable(InverseTest src/InverseTest.cpp)
target_link_libraries(InverseTest PRIVATE Camera SquareMesh SolidRender Affine OpenGL glm::glm SDL2::SDL2 ${GLEW_LIBRARIES})
include_directories(InverseTest ${GLEW_INCLUDE_DIRS})

add_library(Texture src/Texture.cpp)
target_link_libraries(Texture PRIVATE Camera SquareMesh SolidRender Affine OpenGL glm::glm SDL2::SDL2 ${GLEW_LIBRARIES})
include_directories(Texture ${GLEW_INCLUDE_DIRS})

add_executable(TextureDemo src/TextureDemo.cpp)
target_link_libraries(TextureDemo PRIVATE Texture Camera SquareMesh SolidRender Affine OpenGL glm::glm SDL2::SDL2 ${GLEW_LIBRARIES})
include_directories(TextureDemo ${GLEW_INCLUDE_DIRS})

add_executable(TextureTest src/TextureTest.cpp)
target_link_libraries(TextureTest PRIVATE Texture Camera SquareMesh SolidRender Affine OpenGL glm::glm SDL2::SDL2 ${GLEW_LIBRARIES})
include_directories(TextureTest ${GLEW_INCLUDE_DIRS})

# vim:shiftwidth=2:
