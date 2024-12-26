cmake_minimum_required(VERSION 3.10)
project(picotts C)

# Set C standard and position independent code for shared libraries
set(CMAKE_POSITION_INDEPENDENT_CODE ON)
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)

# Add compile definitions
if(WIN32)
    add_definitions(-DPICO_PLATFORM=PICO_Windows)
else()
    add_definitions(-DPICO_PLATFORM=PICO_POSIX)
endif()

# Include directories
include_directories(
    ${CMAKE_SOURCE_DIR}/lib
    ${CMAKE_SOURCE_DIR}/compat/include
)

# Add library subdirectory
add_subdirectory(lib)

# Find popt library using pkg-config
find_package(PkgConfig REQUIRED)
pkg_check_modules(POPT REQUIRED popt)

# Add the pico2wave executable
add_executable(pico2wave
    bin/pico2wave.c
    lib/picoos.c    
    lib/picoapi.c    
    lib/picopal.c    
    lib/picorsrc.c
    lib/picoctrl.c
    lib/picodata.c
    lib/picotrns.c
    lib/picokfst.c
    lib/picoknow.c
lib/picokpr.c
lib/picoktab.c
lib/picoklex.c
lib/picokdt.c
lib/picokpdf.c
lib/picotok.c
lib/picowa.c
lib/picosa.c
lib/picoacph.c
lib/picospho.c
lib/picopam.c
lib/picocep.c
lib/picosig.c
lib/picosig2.c
lib/picobase.c
lib/picopr.c
lib/picofftsg.c

)

# Make sure picolib is built before pico2wave
add_dependencies(pico2wave picolib)

# Link pico2wave with picolib (the DLL directly) and popt
target_link_libraries(pico2wave
    PRIVATE
        picolib # Link with picolib using the target name
        ${POPT_LIBRARIES}
)

# Add the directory where picolib (the DLL) will be built to the runtime path
target_link_directories(pico2wave
    PRIVATE
        $<TARGET_FILE_DIR:picolib> # Use generator expression to get DLL directory
)

target_include_directories(pico2wave
    PRIVATE
        ${POPT_INCLUDE_DIRS}
)

# Installation rules
install(TARGETS pico2wave
    RUNTIME DESTINATION bin
)

# Install language files
file(GLOB LANG_FILES "lang/*.bin")
install(FILES ${LANG_FILES}
    DESTINATION share/pico/lang
)
