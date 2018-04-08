cmake_minimum_required(VERSION 3.10)
project(OpenGLLearning)

IF(NOT CMAKE_BUILD_TYPE)
    SET(CMAKE_BUILD_TYPE Debug CACHE STRING "Choose the type of build (Debug or Release)" FORCE)
ENDIF(NOT CMAKE_BUILD_TYPE)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/modules/")

if(WIN32)
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)
endif(WIN32)

link_directories(${CMAKE_SOURCE_DIR}/lib)

list(APPEND CMAKE_CXX_FLAGS "-std=c++11")

# find the required packages
find_package(glfw3 REQUIRED)
message(STATUS "Found GLFW3 in ${GLFW3_INCLUDE_DIR}")

set(LIBS glfw3 opengl32)


# first create relevant static libraries requried for other projects
add_library(GLAD "lib/glad.c")
set(LIBS ${LIBS} GLAD)

include_directories(${CMAKE_SOURCE_DIR}/includes)

add_executable(OpenGLLearning src/main.cpp)

target_link_libraries(OpenGLLearning ${LIBS})