cmake_minimum_required(VERSION 3.25)
project(imgui)

set(CMAKE_CXX_STANDARD 23)

# TRYING TO PULL SYSTEM"S openGL may be a very bad idea, since raylib is already using its own.
#

set(IMGUI_PATH  "${CMAKE_CURRENT_SOURCE_DIR}")
message("${IMGUI_PATH}")
    
# Compile as static library
file(GLOB IMGUI_SOURCES "${IMGUI_PATH}/*.cpp")
add_library(ImGui STATIC "${IMGUI_SOURCES}")
target_include_directories(ImGui PUBLIC "${IMGUI_PATH}")
target_link_libraries(ImGui PRIVATE glfw)

# Try to build one of the example executables.
set(BACKENDS_INCLUDE_DIRS
        "${CMAKE_CURRENT_SOURCE_DIR}/backends/")
file(GLOB BACKENDS_SOURCES
        "${CMAKE_CURRENT_SOURCE_DIR}/backends/*.cpp")



add_executable(imgui_glfw_opengl3)
target_sources(imgui_glfw_opengl3
                    PRIVATE
                    "${CMAKE_CURRENT_SOURCE_DIR}/examples/example_glfw_opengl3/main.cpp"
                    "${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_opengl3.cpp"
                    "${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_glfw.cpp"
                    "${IMGUI_SOURCES}")

target_include_directories(imgui_glfw_opengl3
                                PRIVATE
                                "${BACKENDS_INCLUDE_DIRS}"
                                "${CMAKE_CURRENT_SOURCE_DIR}"
        )

target_link_libraries(imgui_glfw_opengl3 PRIVATE glfw)
target_link_libraries(imgui_glfw_opengl3 PRIVATE opengl32)

