# Set the minimum required version of CMake
cmake_minimum_required(VERSION 3.20)
PROJECT(hackrf)

# Include the libfftw3 in single precision mode (libfftw3)
set(libfftw3 fftw3f)
add_subdirectory(libs/fftw-3.3.10)

# add library called libhackrf
set(libhackrf hackrf)
add_library(${libhackrf} SHARED
        ${CMAKE_CURRENT_SOURCE_DIR}/src/main/jni/hackrf_wrapper.c)

# Specify public include directories for libhackrf
target_include_directories(${libhackrf} PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/src/main/jni)

# Link the libhackrf library
target_link_libraries(
		${libhackrf}
        log
)