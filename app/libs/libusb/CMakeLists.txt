# Set the minimum required version of CMake
cmake_minimum_required(VERSION 3.20)
project(libusb)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fvisibility=hidden -pthread")

set(LOCAL_CFLAGS "${LOCAL_CFLAGS} \
  -std=gnu11 \
  -Wall \
  -Wextra \
  -Wshadow \
  -Wunused \
  -Wwrite-strings \
  -Werror=format-security \
  -Werror=implicit-function-declaration \
  -Werror=implicit-int \
  -Werror=init-self \
  -Werror=missing-prototypes \
  -Werror=strict-prototypes \
  -Werror=undef \
  -Werror=uninitialized")

# Define library with libusb sources
set(libusb usb)
add_library(${libusb} STATIC
        ${CMAKE_CURRENT_SOURCE_DIR}/core.c
        ${CMAKE_CURRENT_SOURCE_DIR}/descriptor.c
        ${CMAKE_CURRENT_SOURCE_DIR}/hotplug.c
        ${CMAKE_CURRENT_SOURCE_DIR}/io.c
        ${CMAKE_CURRENT_SOURCE_DIR}/sync.c
        ${CMAKE_CURRENT_SOURCE_DIR}/strerror.c
        ${CMAKE_CURRENT_SOURCE_DIR}/os/linux_usbfs.c
        ${CMAKE_CURRENT_SOURCE_DIR}/os/events_posix.c
        ${CMAKE_CURRENT_SOURCE_DIR}/os/threads_posix.c
        ${CMAKE_CURRENT_SOURCE_DIR}/os/linux_netlink.c)

# Include directories
target_include_directories(${libusb} PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}
        ${CMAKE_CURRENT_SOURCE_DIR}/os)

# Link against log library
target_link_libraries(${libusb} log)