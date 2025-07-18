cmake_minimum_required(VERSION 3.20)
project(node_editor VERSION 0.1)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# -----------------------------------------------------------------------------
# Collect ImGui source files to be built with the main executable
# -----------------------------------------------------------------------------
file(GLOB IMGUI_SRC
    external/imgui/imgui*.cpp
    external/imgui/backends/imgui_impl_glfw.cpp
    external/imgui/backends/imgui_impl_opengl3.cpp
)

# -----------------------------------------------------------------------------
# Main source files
# -----------------------------------------------------------------------------
set(SOURCE_FILES
    src/main.cpp
    ${IMGUI_SRC}
)

# -----------------------------------------------------------------------------
# Precompiled Headers (Optional)
# -----------------------------------------------------------------------------
set(PCH_FILES
    src/core/pch.h
)

# -----------------------------------------------------------------------------
# GLFW (vendored)
# -----------------------------------------------------------------------------
add_subdirectory(external/glfw)

# -----------------------------------------------------------------------------
# GLM (vendored)
# -----------------------------------------------------------------------------
add_subdirectory(external/glm)


# ---------------------------------------------------------
# GLAD (Open GL Wrapper)
# ---------------------------------------------------------
add_library(glad STATIC external/glad/src/glad.c)
target_include_directories(glad PUBLIC external/glad/include)

# -----------------------------------------------------------------------------
# Executable Target
# -----------------------------------------------------------------------------
add_executable(${PROJECT_NAME} ${SOURCE_FILES})
target_precompile_headers(${PROJECT_NAME} PRIVATE ${PCH_FILES})


# -----------------------------------------------------------------------------
# Includes
# -----------------------------------------------------------------------------
target_include_directories(${PROJECT_NAME}
    PUBLIC SRC
    PUBLIC external
    PUBLIC external/glfw/include
)

# -----------------------------------------------------------------------------
# Compiler Options
# -----------------------------------------------------------------------------
target_compile_options(${PROJECT_NAME} PRIVATE -Wall -Wextra -pedantic)

# -----------------------------------------------------------------------------
# Link Libraries
# -----------------------------------------------------------------------------
target_link_libraries(${PROJECT_NAME}
    glfw
    glad
    glm
    ${CMAKE_DL_LIBS}
)
