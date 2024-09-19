cmake_minimum_required(VERSION 3.27)
project(include/sqlite_modern_cpp VERSION 1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(sqlite_modern_cpp INTERFACE)

target_include_directories(sqlite_modern_cpp
  INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>
)

include(CMakePackageConfigHelpers)
configure_package_config_file(
  "${CMAKE_CURRENT_SOURCE_DIR}/sqlite_modern_cppConfig.cmake.in"
  "${CMAKE_CURRENT_BINARY_DIR}/sqlite_modern_cppConfig.cmake"
  INSTALL_DESTINATION share/sqlite_modern_cpp
)

install(TARGETS sqlite_modern_cpp
  EXPORT sqlite_modern_cppTargets
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)

install(DIRECTORY ${CMAKE_SOURCE_DIR}/include/sqlite_modern_cpp DESTINATION include)
install(FILES ${CMAKE_SOURCE_DIR}/include/sqlite_modern_cpp.h DESTINATION include)

install(
  EXPORT sqlite_modern_cppTargets
  DESTINATION share/sqlite_modern_cpp
  NAMESPACE sqlite_modern_cpp::
)

install(
  FILES
  "${CMAKE_CURRENT_BINARY_DIR}/sqlite_modern_cppConfig.cmake"
  DESTINATION share/sqlite_modern_cpp
)