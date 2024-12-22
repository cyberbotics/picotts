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

# Create the library
add_library(picolib STATIC ${PICO_SOURCES})

# Set include directories for the library
target_include_directories(picolib PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
)

# Link with required system libraries
target_link_libraries(picolib
    m  # Math library
)
