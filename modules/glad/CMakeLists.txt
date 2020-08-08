cmake_minimum_required(VERSION 3.7)

project(glad)

# Set compiler flags
if(CMAKE_COMPILER_IS_GNUCC)
	set(CMAKE_CXX_FLAGS "-Wall -Wextra")
	set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS} -g")
	set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS} -O3")
elseif(MSVC)
	set(CMAKE_C_FLAGS "/W3 /MP /MT")
	set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS}")
	set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS} /Ox")
endif()

add_library(${PROJECT_NAME} ${PROJECT_SOURCE_DIR}/glad.c)

# Install library
install(TARGETS ${PROJECT_NAME}
	EXPORT ${PROJECT_NAME}-targets
	ARCHIVE DESTINATION lib
	LIBRARY DESTINATION lib
	RUNTIME DESTINATION bin)

# Install headers
install(
	FILES
		${PROJECT_SOURCE_DIR}/glad.h
		${PROJECT_SOURCE_DIR}/khrplatform.h
	DESTINATION include/glad)

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
