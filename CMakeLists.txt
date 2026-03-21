cmake_minimum_required(VERSION 3.24...3.25)

project(obs-qsv-onevpl
  VERSION 1.2.0.0
  LANGUAGES CXX
)

if(NOT PROJECT_IS_TOP_LEVEL)
  if(UNIX)
    add_compile_options(-Wno-error)
  elseif(WIN32)
    set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY COMPILE_WARNING_AS_ERROR OFF)
  endif()
endif()

if(WIN32)
  if(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/oneVPL/CMakeLists.txt")
    set(BUILD_TOOLS OFF CACHE BOOL "" FORCE)
    add_subdirectory(oneVPL)
  elseif(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/libvpl/CMakeLists.txt")
    set(BUILD_TOOLS OFF CACHE BOOL "" FORCE)
    add_subdirectory(libvpl)
  else()
    find_package(VPL REQUIRED)
  endif()
endif()

add_subdirectory(libvpl-private)
add_subdirectory(obs-qsvonevpl)
