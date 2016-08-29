cmake_minimum_required(VERSION 3.5)
project(glfw_init)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

find_package(OpenGL)
if(OPENGL_FOUND)
    message(STATUS "Found OpenGL")
endif(OPENGL_FOUND)

#find_package(glfw3 3 REQUIRED) #-- does not work --
find_package(PkgConfig REQUIRED)
pkg_search_module(GLFW REQUIRED glfw3)
if(GLFW_FOUND)
    message(STATUS "Found GLFW")
    message(STATUS "GLFW_INCLUDE_DIRS:    " ${GLFW_INCLUDE_DIRS} )
    message(STATUS "GLFW_LIBRARIES:    " ${GLFW_LIBRARIES} )
endif(GLFW_FOUND)

include_directories(${GLFW_INCLUDE_DIRS})
link_directories(${GLFW_LIBRARY_DIRS})

set(SOURCE_FILES main.cpp)

add_executable(glfw_init ${SOURCE_FILES})

########################################################
# Linking & stuff
#########################################################
target_link_libraries(glfw_init ${GLFW_LIBRARIES} ${OPENGL_gl_LIBRARY})