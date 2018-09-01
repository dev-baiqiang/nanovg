cmake_minimum_required(VERSION 3.3)
project(nanovg)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

set(SOURCE_FILES
        example/demo.c
        example/example_gl3.c
        example/perf.c
        src/fontstash.h
        src/nanovg.c
        src/nanovg.h
        src/nanovg_gl.h
        src/nanovg_gl_utils.h
        src/stb_image.h
        src/stb_truetype.h)


add_executable(nanovg ${SOURCE_FILES})

find_package(OpenGL REQUIRED)
find_package(glfw REQUIRED)

target_link_libraries(nanovg ${OPENGL_LIBRARIES} ${GLFW_LIBRARIES})
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/src /usr/local/include ${OPENGL_INCLUDE_DIRS} ${GLFW_INCLUDE_DIRS})

add_custom_command(TARGET nanovg PRE_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_directory ${CMAKE_SOURCE_DIR}/example
        $<TARGET_FILE_DIR:nanovg>/example
)