cmake_minimum_required(VERSION 3.10)
project(picotts C)

# Set C standard and position independent code for shared libraries
set(CMAKE_POSITION_INDEPENDENT_CODE ON)
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)

# Add compile definitions
add_definitions(-DPICO_PLATFORM=PICO_POSIX)
add_definitions(-DINSTALL_PATH=".")

# Include directories
include_directories(
    ${CMAKE_SOURCE_DIR}/lib
    ${CMAKE_SOURCE_DIR}/compat/include
)

# Add library subdirectory
add_subdirectory(lib)

# Find popt library
find_library(POPT_LIBRARY NAMES popt)
if(NOT POPT_LIBRARY)
    message(FATAL_ERROR "popt library not found")
endif()

# Add the pico2wave executable
add_executable(pico2wave bin/pico2wave.c)
target_link_libraries(pico2wave picolib ${POPT_LIBRARY})

# Installation rules
install(TARGETS pico2wave
    RUNTIME DESTINATION bin
)

# Install language files
file(GLOB LANG_FILES "lang/*.bin")
install(FILES ${LANG_FILES}
    DESTINATION share/pico/lang
)
