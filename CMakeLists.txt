cmake_minimum_required(VERSION 3.12)

include("./CMakeShared.txt")

set(PROJ_NAME pr_xatlas)

project(${PROJ_NAME} CXX)

# set(PRECOMPILED_HEADER "stdafx")

link_external_library(xatlas)
link_external_library(vfilesystem)
link_external_library(sharedutils)
link_external_library(mathutil)
link_external_library(ishared)
add_external_library(luajit)
if(WIN32)
	add_external_library(lua)
endif()
add_include_dir(glm)

set(DEPENDENCY_XATLAS_INCLUDE ${CMAKE_CURRENT_LIST_DIR}/third_party/xatlas/source/xatlas CACHE PATH "" FORCE)
search_lib_recursive(DEPENDENCY_XATLAS_LIBRARY third_party/xatlas/${BINARY_PRAGMA_DIR} xatlas STATIC)

link_generic_module_libraries()
register_pragma_module(${PROJ_NAME})

add_subdirectory(third_party/xatlas)
set_target_properties(xatlas PROPERTIES FOLDER third_party)
add_dependencies(${PROJ_NAME} xatlas vfilesystem sharedutils mathutil ishared luasystem)
