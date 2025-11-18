cmake_minimum_required(VERSION 3.13...4.0)

project(glpng C)
include(GNUInstallDirs)

set(SONAME_VERSION 1)
set(MINOR_VERSION 47)
set(VERSION ${SONAME_VERSION}.${MINOR_VERSION})

find_package(PNG REQUIRED)
find_package(OpenGL REQUIRED)

add_link_options(LINKER:-z,defs)

add_subdirectory(src)
configure_file(FindGLPNG.cmake.in FindGLPNG.cmake @ONLY)

install(FILES include/GL/glpng.h DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/GL/)
install(FILES glpng.htm DESTINATION ${CMAKE_INSTALL_DOCDIR})
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/FindGLPNG.cmake DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/cmake/Modules)

if(PROJECT_IS_TOP_LEVEL)
  add_subdirectory(Example)
endif()
