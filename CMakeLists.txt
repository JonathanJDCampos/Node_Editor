cmake_minimum_required(VERSION 3.20)
project(node_editor VERSION 0.1)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# -----------------------------------------------------------------------------
# Collect ImGui source files to be built with the main executable
# -----------------------------------------------------------------------------
file(GLOB NODE_EDITOR_SRC
    # external/imgui/imgui*.cpp
    # external/imgui/backends/imgui_impl_glfw.cpp
    # external/imgui/backends/imgui_impl_opengl3.cpp
    external/imgui-node-editor/*.cpp
    external/imgui-node-editor/external/imgui/*.cpp
)

file(GLOB EXAMPLES_APPLICATION_SRC
    external/imgui-node-editor/examples/application/source/application.cpp
    external/imgui-node-editor/examples/application/source/renderer_ogl3.cpp
    external/imgui-node-editor/examples/application/source/entry_point.cpp
    external/imgui-node-editor/examples/application/source/imgui_impl_glfw.cpp
    external/imgui-node-editor/examples/application/source/imgui_impl_opengl3.cpp
    external/imgui-node-editor/examples/application/source/platform_glfw.cpp
)

file(GLOB BLUEPRINT_EXAMPLE_SRC
    external/imgui-node-editor/examples/blueprints-example/blueprints-example.cpp
    external/imgui-node-editor/examples/blueprints-example/utilities/builders.cpp
    external/imgui-node-editor/examples/blueprints-example/utilities/drawing.cpp
    external/imgui-node-editor/examples/blueprints-example/utilities/widgets.cpp
)


# -----------------------------------------------------------------------------
# Main source files
# -----------------------------------------------------------------------------
set(SOURCE_FILES
    ${NODE_EDITOR_SRC}
    ${EXAMPLES_APPLICATION_SRC}
    ${BLUEPRINT_EXAMPLE_SRC}
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
    PUBLIC external/imgui-node-editor
    PUBLIC external/imgui-node-editor/external/imgui
    PUBLIC external/imgui-node-editor/examples/application/include
    PUBLIC external/imgui-node-editor/external/stb_image
)

# -----------------------------------------------------------------------------
# Compiler Options
# -----------------------------------------------------------------------------
target_compile_options(${PROJECT_NAME} PRIVATE -Wall -Wextra -pedantic)

if (WIN32)
target_compile_definitions(${PROJECT_NAME} PRIVATE
        HAVE_OPENGL=1
        HAVE_GLFW3=1            # only if you're actually using GLFW
        RENDERER_CONFIG=IMGUI_OGL3
        BACKEND_CONFIG=IMGUI_GLFW  # omit or change if using Win32 platform
        IMGUI_IMPL_OPENGL_LOADER_GLAD=1
    )
endif()



# -----------------------------------------------------------------------------
# Link Libraries
# -----------------------------------------------------------------------------
target_link_libraries(${PROJECT_NAME}
    glfw
    glad
    glm
    ${CMAKE_DL_LIBS}
    imm32
)