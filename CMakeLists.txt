cmake_minimum_required(VERSION 3.5)

project(wxWidgetsTask LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Set OpenGL preference to GLVND to avoid warnings
cmake_policy(SET CMP0072 NEW)
set(OpenGL_GL_PREFERENCE "GLVND")

# Find wxWidgets with OpenGL support
find_package(wxWidgets REQUIRED COMPONENTS gl core base)
include(${wxWidgets_USE_FILE})

# Find OpenGL
find_package(OpenGL REQUIRED)
find_package(GLEW REQUIRED)

# Add the executable
add_executable(wxWidgetsTask main.cpp glcanvas.h glcanvas.cpp)

# Link necessary libraries
target_link_libraries(wxWidgetsTask
    ${wxWidgets_LIBRARIES}
    OpenGL::GL
    OpenGL::GLX  # Ensure proper linking with GLX
    GLU
    GLEW::GLEW
)

# Installation settings
include(GNUInstallDirs)
install(TARGETS wxWidgetsTask
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
