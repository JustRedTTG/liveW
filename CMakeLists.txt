cmake_minimum_required(VERSION 3.30)
project(livew)

set(CMAKE_CXX_STANDARD 20)

find_package(OpenGL REQUIRED)
find_package(X11 REQUIRED)
find_package(Freetype REQUIRED)
find_package(PkgConfig REQUIRED)
find_package(FFTW3 REQUIRED)
pkg_check_modules(PULSEAUDIO REQUIRED libpulse-simple)

include_directories(
        ${OPENGL_INCLUDE_DIR}
        ${X11_INCLUDE_DIR}
        ${FREETYPE_INCLUDE_DIRS}
        ${PULSEAUDIO_INCLUDE_DIRS}
        ${FFTW3_INCLUDES}
        "include"
)

add_executable(livew
        src/main.c
        src/config.c
        src/renderer.c
        src/utils.c
        src/xwin.c
)

target_link_libraries(livew
        ${OPENGL_LIBRARIES}  # OpenGL dependencies
        GL                   # OpenGL core library
        ${X11_LIBRARIES}     # X11 dependencies
        X11                  # X11 core library
        Xrender              # X11 rendering library
        ${FREETYPE_LIBRARIES} # Freetype dependencies
        freetype              # Freetype core library
        ${PULSEAUDIO_LIBRARIES} # PipeWire dependencies
        ${FFTW3_LIBRARIES}     # FFTW3 dependencies
        m                    # Math library (libm)
)

target_compile_options(livew PRIVATE -Wall -Wextra -pedantic)