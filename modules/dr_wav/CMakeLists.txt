cmake_minimum_required(VERSION 3.7)

project(dr_wav)

add_library(dr_wav ${PROJECT_SOURCE_DIR}/dr_wav.cpp)

# Install library
install(TARGETS ${PROJECT_NAME}
	EXPORT ${PROJECT_NAME}-targets
	ARCHIVE DESTINATION lib
	LIBRARY DESTINATION lib
	RUNTIME DESTINATION bin)

# Install header
install(
	FILES ${PROJECT_SOURCE_DIR}/dr_wav.h
	DESTINATION include/dr_libs)

# Install CMake config file
install(EXPORT ${PROJECT_NAME}-targets
	FILE ${PROJECT_NAME}-targets.cmake
	DESTINATION lib/cmake/${PROJECT_NAME})

include(CMakePackageConfigHelpers)
configure_package_config_file(
    ${PROJECT_SOURCE_DIR}/${PROJECT_NAME}-config.cmake.in
    ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config.cmake
    INSTALL_DESTINATION lib/cmake/${PROJECT_NAME})

install(
    FILES ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config.cmake
    DESTINATION lib/cmake/${PROJECT_NAME})
