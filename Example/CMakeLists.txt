
project(Test C)


find_package(OpenGL REQUIRED)
find_package(GLUT REQUIRED)

set(target Test)
add_executable(${target} Test.c)
# target_compile_features(${target} PRIVATE c_std_23)
target_link_libraries(${target} PRIVATE glpng)
target_link_libraries(${target} PRIVATE OpenGL::GL OpenGL::GLU)
target_link_libraries(${target} PRIVATE GLUT::GLUT)
add_custom_command(TARGET ${target} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy 
        ${CMAKE_CURRENT_SOURCE_DIR}/Stunt.png
        $<TARGET_FILE_DIR:${target}>/)
