get_filename_component(FolderName ${CMAKE_CURRENT_SOURCE_DIR} NAME)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_RELWITHDEBINFO ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_MINSIZEREL ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/lib)

set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_RELWITHDEBINFO ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_MINSIZEREL ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/lib)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELWITHDEBINFO ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_MINSIZEREL ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/lib)

file(GLOB_RECURSE SrcFiles *.cpp)
file(GLOB_RECURSE HeaderFiles *.h *.build *.include *.hpp)
set(AllFiles ${SrcFiles} ${HeaderFiles})

add_library(${FolderName} STATIC ${SrcFiles})
add_library(${PROJECT_NAME}::${FolderName} ALIAS ${FolderName})

target_include_directories(${FolderName}
    PUBLIC 
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    $<INSTALL_INTERFACE:include>
)

# install settings
install(TARGETS ${FolderName} 
    EXPORT ${FolderName}Targets
    RUNTIME DESTINATION "bin"
    LIBRARY DESTINATION "lib"
    ARCHIVE DESTINATION "lib"
)

install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/${PROJECT_NAME} DESTINATION "include"
        FILES_MATCHING PATTERN "*.h")

install(EXPORT ${FolderName}Targets
    FILE ${FolderName}Targets.cmake
    NAMESPACE ${PROJECT_NAME}::
    DESTINATION lib/cmake/${PROJECT_NAME}
)

include(CMakePackageConfigHelpers)
# generate the config file that is includes the exports
configure_package_config_file(${CMAKE_CURRENT_SOURCE_DIR}/${FolderName}Config.cmake.in
    "${CMAKE_CURRENT_BINARY_DIR}/${FolderName}Config.cmake"
    INSTALL_DESTINATION "lib/cmake/${PROJECT_NAME}"
)
# generate the version file for the config file
write_basic_package_version_file(
    "${CMAKE_CURRENT_BINARY_DIR}/${FolderName}ConfigVersion.cmake"
    VERSION "${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}"
    COMPATIBILITY AnyNewerVersion
)

install(FILES
    ${CMAKE_CURRENT_BINARY_DIR}/${FolderName}Config.cmake
    ${CMAKE_CURRENT_BINARY_DIR}/${FolderName}ConfigVersion.cmake
    DESTINATION lib/cmake/${PROJECT_NAME}
)

export(EXPORT ${FolderName}Targets FILE ${CMAKE_CURRENT_BINARY_DIR}/${FolderName}Targets.cmake NAMESPACE ${PROJECT_NAME}::)
