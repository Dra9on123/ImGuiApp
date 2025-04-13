cmake_minimum_required(VERSION 3.12)
project(ImGuiApp)

set(CMAKE_CXX_STANDARD 17)

file(GLOB IMGUI_SOURCES
    thirdparty/imgui/imgui.cpp
    thirdparty/imgui/imgui_draw.cpp
    thirdparty/imgui/imgui_tables.cpp
    thirdparty/imgui/imgui_widgets.cpp
    thirdparty/imgui/imgui_demo.cpp
    thirdparty/imgui/backends/imgui_impl_glfw.cpp
    thirdparty/imgui/backends/imgui_impl_opengl3.cpp
)

add_library(imgui STATIC ${IMGUI_SOURCES})

target_include_directories(imgui PUBLIC
    thirdparty/imgui
    thirdparty/imgui/backends
    thirdparty/glfw/include 
)


add_subdirectory(thirdparty/glfw)

add_executable(ImGuiApp
    src/main.cpp
)



target_link_libraries(ImGuiApp PRIVATE imgui glfw)

find_package(OpenGL REQUIRED)
target_link_libraries(ImGuiApp PRIVATE OpenGL::GL)
