cmake_minimum_required(VERSION 3.10.2)
project(renderer)

find_package(OpenGL REQUIRED)
find_package(GLUT REQUIRED)

if(OPENGL_FOUND)
    message("opengl found")
    message("include dir: ${OPENGL_INCLUDE_DIR}")
    message("link libraries: ${OPENGL_gl_LIBRARY}")
else (OPENGL_FOUND)
    message("opengl not found")
endif()

set(SOURCES src/main.cpp)

add_executable(filter ${SOURCES})

add_dependencies(filter OpenGL::OpenGL)
target_include_directories(filter PUBLIC src)
target_include_directories(filter PRIVATE ${OPENGL_INCLUDE_DIR})
target_include_directories(filter PRIVATE ${GLUT_INCLUDE_DIRS} )

target_link_libraries(filter OpenGL::OpenGL ${OPENGL_glu_LIBRARY})
target_link_libraries(filter OpenGL::OpenGL ${GLUT_LIBRARY})

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -lglut -lGLU -lGL")
