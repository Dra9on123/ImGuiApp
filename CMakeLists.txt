cmake_minimum_required(VERSION 3.20)
project(ImGuiApp)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(SDL_TEST OFF CACHE BOOL "" FORCE)
set(SDL_SHARED OFF CACHE BOOL "" FORCE)
set(SDL_STATIC ON CACHE BOOL "" FORCE)

add_subdirectory(thirdparty/sdl EXCLUDE_FROM_ALL)

set(SDL_INCLUDE_DIRS
    ${CMAKE_CURRENT_SOURCE_DIR}/thirdparty/sdl/include
    ${CMAKE_BINARY_DIR}/thirdparty/sdl/include
)

file(GLOB IMGUI_SOURCES
    thirdparty/imguidocking/imgui.cpp
    thirdparty/imguidocking/imgui_draw.cpp
    thirdparty/imguidocking/imgui_tables.cpp
    thirdparty/imguidocking/imgui_widgets.cpp
    thirdparty/imguidocking/imgui_demo.cpp
    thirdparty/imguidocking/backends/imgui_impl_sdl2.cpp
    thirdparty/imguidocking/backends/imgui_impl_opengl3.cpp
)

add_library(imguidocking STATIC ${IMGUI_SOURCES})

target_include_directories(imguidocking PUBLIC
    thirdparty/imguidocking
    thirdparty/imguidocking/backends
    ${SDL_INCLUDE_DIRS}
)

add_executable(ImGuiApp
    src/main.cpp
)

# Required to avoid SDL redefining `main`
target_compile_definitions(ImGuiApp PRIVATE SDL_MAIN_HANDLED)

target_include_directories(ImGuiApp PRIVATE ${SDL_INCLUDE_DIRS})

find_package(OpenGL REQUIRED)

target_link_libraries(ImGuiApp PRIVATE
    imguidocking
    SDL2-static
    OpenGL::GL
)
