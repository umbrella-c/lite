cmake_minimum_required(VERSION 3.8)
project(lite C)

set (CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set (CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set (CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)

include_directories(src/api src)

# Configure primary executable target
add_executable(lite 
    src/api/api.c
    src/api/renderer_font.c
    src/api/renderer.c
    src/api/system.c
    
    src/lib/stb/stb_truetype.c
    
    src/main.c
    src/rencache.c
    src/renderer.c)
if (MOLLENOS)
  include_directories(../)
  target_link_libraries(lite SDL2 liblua)
else ()
  target_link_libraries(lite sdl)
endif()

# Add a new install target
install(TARGETS lite DESTINATION bin)
install(DIRECTORY data DESTINATION share/lite)
