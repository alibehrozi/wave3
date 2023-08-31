# Set the minimum required version of CMake
cmake_minimum_required(VERSION 3.20)
PROJECT(hackrf)

# Include the libusb
set(libusb usb)
add_subdirectory(libs/libusb)

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