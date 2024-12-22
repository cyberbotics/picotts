# Collect all source files
set(PICO_SOURCES
    picoacph.c
    picoapi.c
    picobase.c
    picocep.c
    picoctrl.c
    picodata.c
    picodbg.c
    picoextapi.c
    picofftsg.c
    picokdbg.c
    picokdt.c
    picokfst.c
    picoklex.c
    picoknow.c
    picokpdf.c
    picokpr.c
    picoktab.c
    picoos.c
    picopal.c
    picopam.c
    picopr.c
    picorsrc.c
    picosa.c
    picosig.c
    picosig2.c
    picospho.c
    picotok.c
    picotrns.c
    picowa.c
)

# Create the shared library
add_library(picolib SHARED ${PICO_SOURCES})
set_target_properties(picolib PROPERTIES
    VERSION 1.0.0
    SOVERSION 1
    OUTPUT_NAME "pico"
)

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
    RUNTIME DESTINATION lib  # For Windows DLL
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
