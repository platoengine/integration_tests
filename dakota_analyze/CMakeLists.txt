include( ${CMAKE_CURRENT_SOURCE_DIR}/../utilities/cmake/tools.cmake )

Set_binaries()
Copy_cmake_utilities_to_binary_dir()

add_subdirectory(examples)
add_subdirectory(regression)
