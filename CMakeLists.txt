cmake_minimum_required(VERSION 3.12)
project(ImGuiApp)

set(CMAKE_CXX_STANDARD 17)

file(GLOB IMGUI_SOURCES
    thirdparty/imguidocking/imgui.cpp
    thirdparty/imguidocking/imgui_draw.cpp
    thirdparty/imguidocking/imgui_tables.cpp
    thirdparty/imguidocking/imgui_widgets.cpp
    thirdparty/imguidocking/imgui_demo.cpp
    thirdparty/imguidocking/backends/imgui_impl_glfw.cpp
    thirdparty/imguidocking/backends/imgui_impl_opengl3.cpp
)

add_library(imguidocking STATIC ${IMGUI_SOURCES})

target_include_directories(imguidocking PUBLIC
    thirdparty/imguidocking
    thirdparty/imguidocking/backends
    thirdparty/glfw/include 
)

add_subdirectory(thirdparty/glfw)

add_executable(ImGuiApp
    src/main.cpp
)

target_link_libraries(ImGuiApp PRIVATE
    imguidocking
    glfw
)

find_package(OpenGL REQUIRED)
target_link_libraries(ImGuiApp PRIVATE OpenGL::GL)

