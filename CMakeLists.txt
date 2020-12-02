cmake_minimum_required(VERSION 3.10.0)
project(my_componet_lib VERSION 0.1.0 LANGUAGES CXX)

add_subdirectory(componet1)
add_subdirectory(componet2)

configure_file(${PROJECT_NAME}Config.cmake.in 
  "${CMAKE_BINARY_DIR}/${PROJECT_NAME}Config.cmake"
  @ONLY
)

include(CMakePackageConfigHelpers)
# generate the version file for the config file
write_basic_package_version_file(
    "${CMAKE_BINARY_DIR}/${PROJECT_NAME}ConfigVersion.cmake"
    VERSION "${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}"
    COMPATIBILITY AnyNewerVersion
)

install (
    FILES
    "${CMAKE_BINARY_DIR}/${PROJECT_NAME}Config.cmake"
    "${CMAKE_BINARY_DIR}/${PROJECT_NAME}ConfigVersion.cmake"
    DESTINATION lib/cmake/${PROJECT_NAME}
)

