
include(CheckLibraryExists)
check_library_exists(m sqrt "" HAVE_LIB_M)
add_library(glpng glpng.c)

target_include_directories(
	glpng
	PUBLIC
	$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/include>
	$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)

target_link_libraries(
	glpng
	PUBLIC
	PNG::PNG
	OpenGL::GL
	$<IF:${HAVE_LIB_M},m,>
)

set_target_properties(glpng PROPERTIES VERSION ${VERSION} SOVERSION ${SONAME_VERSION})
install(TARGETS glpng DESTINATION ${CMAKE_INSTALL_LIBDIR})
