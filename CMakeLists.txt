cmake_minimum_required(VERSION 3.30)
project("Game of Life C++ Implementation" VERSION 0.1 LANGUAGES CXX DESCRIPTION "Game of Life C++ Implementation with the most recent C++ standard")

include(GNUInstallDirs)
include(CMakePackageConfigHelpers)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_INSTALL_RPATH $<INSTALL_INTERFACE:${CMAKE_INSTALL_LIBDIR}>)

enable_testing()

file(GLOB source_files RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} src/*.cpp)
file(GLOB header_files RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} include/**/*.hpp)
file(GLOB test_files RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} test/*.cpp)

add_library(life SHARED)
target_sources(life INTERFACE FILE_SET HEADERS BASE_DIRS $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include> $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}> FILES ${header_files})
target_sources(life PRIVATE ${source_files})
target_include_directories(life PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include> $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>)
target_compile_definitions(life PRIVATE LIBRARY_VERSION="${PROJECT_VERSION}")

write_basic_package_version_file(${CMAKE_BINARY_DIR}/LifeVersion.cmake VERSION ${PROJECT_VERSION} COMPATIBILITY SameMajorVersion)

install(TARGETS life COMPONENT Library LIBRARY CONFIGURATIONS Release MinSizeRel)
install(FILES ${CMAKE_BINARY_DIR}/LifeVersion.cmake COMPONENT Library CONFIGURATIONS Release MinSizeRel DESTINATION ${CMAKE_INSTALL_LIBDIR}/life/cmake)

set(CPACK_PACKAGE_VENDOR "Brian Salehi")
set(CPACK_PACKAGE_CONTACT "briansalehi@proton.me")
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "${PROJECT_DESCRIPTON}")
set(CPACK_PACKAGE_NAME "life")
string(TOLOWER ${CMAKE_SYSTEM_NAME} CPACK_SYSTEM_NAME)
set(CPACK_DEBIAN_PACKAGE_DEPENDS "")
set(CPACK_RPM_PACKAGE_DEPENDS "")

include(CPack)
