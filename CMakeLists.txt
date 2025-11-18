include(${CMAKE_SOURCE_DIR}/cmake/pr_common.cmake)

set(PROJ_NAME pr_xatlas)
pr_add_module(${PROJ_NAME} SHARED "modules/")

pr_add_dependency(${PROJ_NAME} ishared TARGET PUBLIC)

pr_init_module(${PROJ_NAME})

add_subdirectory(third_party/xatlas)
set_target_properties(xatlas PROPERTIES FOLDER third_party)
pr_add_dependency(${PROJ_NAME} xatlas TARGET PUBLIC)
target_include_directories(${PROJ_NAME} PUBLIC third_party/xatlas/source/xatlas/)

pr_finalize(${PROJ_NAME})
