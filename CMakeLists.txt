cmake_minimum_required(VERSION 3.3)
project(nanovg)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

add_definitions(-DNANOVG_GLEW)

set(SOURCE_FILES
        example/demo.c
        example/example_gl3.c
        src/nanovg.c)


add_executable(nanovg ${SOURCE_FILES})

find_package(OpenGL REQUIRED)
find_package(glfw REQUIRED)
find_package(GLEW REQUIRED)

target_link_libraries(nanovg ${OPENGL_LIBRARIES} ${GLEW_LIBRARIES} ${GLFW_LIBRARIES})
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/src /usr/local/include ${OPENGL_INCLUDE_DIRS} ${GLFW_INCLUDE_DIRS} ${GLFW_INCLUDE_DIRS})

add_custom_command(TARGET nanovg PRE_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_directory ${CMAKE_SOURCE_DIR}/example
        $<TARGET_FILE_DIR:nanovg>/example
)