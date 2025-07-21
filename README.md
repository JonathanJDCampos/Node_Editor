# ImGui Node Editor Example (GLFW + OpenGL3 + CMake on Windows)

This project demonstrates how to integrate the [ImGui Node Editor](https://github.com/thedmd/imgui-node-editor) with a modern OpenGL3 rendering backend and GLFW for window/context creation. It's a minimal, yet complete example intended to help developers quickly get started with node-based UI using [Dear ImGui](https://github.com/ocornut/imgui).

The intended use is as template for other projects.

## ✨ Features

- 🧱 Uses [imgui-node-editor](https://github.com/thedmd/imgui-node-editor)
- 🪟 GLFW for cross-platform window management
- 🔲 Modern OpenGL 3 rendering pipeline
- 🧮 GLM for math/vector/matrix operations (included for later use)
- ⚙️ Built with CMake
- 🖥️ Developed in VS Code with Clang on Windows

---

## 📸 Screenshot

"The following screenshot is taken from the original [ImGui Node Editor](https://github.com/thedmd/imgui-node-editor) repository by @thedmd."

![Node Editor Screenshot](media/screenshot1.gif)

---

## 🚀 Getting Started

### Uses

- [Visual Studio Code](https://code.visualstudio.com/)
- [CMake](https://cmake.org/) >= 3.15
- A C++17-compatible compiler (e.g., Clang or GCC)
- Git

### Dependencies

- [Dear ImGui](https://github.com/ocornut/imgui)
- [imgui-node-editor](https://github.com/thedmd/imgui-node-editor)
- [GLFW](https://www.glfw.org/)
- [GLAD or GLEW](https://glad.dav1d.de/) (OpenGL loader)
- [GLM](https://github.com/g-truc/glm.git) (GLM Mathematics Library)

You can include dependencies manually, or via `git submodules` or `FetchContent`.

---

## 🛠️ Building

1. **Clone this repository:**

   ```bash
   git clone --recursive https://github.com/JonathanJDCampos/Node_Editor.git
   cd Node_Editor
   ```
