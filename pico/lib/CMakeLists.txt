# Use GLOB to find all C source files in the current directory
file(GLOB PICO_SOURCES "*.c")

# Create the shared library
add_library(picolib SHARED ${PICO_SOURCES})
set_target_properties(picolib PROPERTIES
    VERSION 1.0.0
    SOVERSION 1
    OUTPUT_NAME "pico"
)
if(WIN32)
    set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)
endif()
# Set include directories for the library
target_include_directories(picolib PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
)

# Link with required system libraries
target_link_libraries(picolib
    m  # Math library
)

# Install the library
install(TARGETS picolib
    LIBRARY DESTINATION lib
    RUNTIME DESTINATION lib  
    ARCHIVE DESTINATION lib
)

# Install headers
install(FILES
    picoacph.h
    picoapi.h
    picobase.h
    picocep.h
    picoctrl.h
    picodata.h
    picodbg.h
    picodefs.h
    picodsp.h
    picofftsg.h
    picokdbg.h
    picokdt.h
    picokfst.h
    picoklex.h
    picoknow.h
    picokpdf.h
    picokpr.h
    picoktab.h
    picoos.h
    picopal.h
    picopam.h
    picopltf.h
    picopr.h
    picorsrc.h
    picosa.h
    picosig.h
    picosig2.h
    picospho.h
    picotok.h
    picotrns.h
    picowa.h
    DESTINATION include/picotts
)
