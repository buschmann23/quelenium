cmake_minimum_required(VERSION 3.1.0 FATAL_ERROR)
cmake_policy(SET CMP0048 NEW)

project(Quelenium VERSION 0.2.0)

find_package(Qt5 5.6.0 REQUIRED COMPONENTS Core Network)

# Auto generate moc files
set(CMAKE_AUTOMOC ON)

set(CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake/modules)

# As moc files are generated in the binary dir, tell CMake
# to always look for includes there:
set(CMAKE_INCLUDE_CURRENT_DIR ON)

if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
  set(CMAKE_INSTALL_PREFIX "/usr/local" CACHE PATH "Quelenium default install prefix" FORCE)
endif(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)

set(CMAKE_INSTALL_LIBDIR "${CMAKE_INSTALL_PREFIX}/lib/${CMAKE_LIBRARY_ARCHITECTURE}" CACHE PATH "Output directory for libraries")

# cmake config files
configure_file(${CMAKE_MODULE_PATH}/Quelenium-config.cmake.in
    ${CMAKE_CURRENT_BINARY_DIR}/QueleniumConfig.cmake
    @ONLY
)
configure_file(${CMAKE_MODULE_PATH}/Quelenium-config-version.cmake.in
    ${CMAKE_CURRENT_BINARY_DIR}/QueleniumConfigVersion.cmake
    @ONLY
)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/QueleniumConfig.cmake
    ${CMAKE_CURRENT_BINARY_DIR}/QueleniumConfigVersion.cmake
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/Quelenium/
)

add_subdirectory(selenium)
