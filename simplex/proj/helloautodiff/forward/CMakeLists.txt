file(GLOB_RECURSE CPPFILES RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} *.cpp)
include(${PROJECT_SOURCE_DIR}/../../script/functions.cmake)
foreach(CPPFILE ${CPPFILES})
    get_filename_component(CPPNAME ${CPPFILE} NAME_WE)
    init_target(${CPPNAME})
    use_ext_libs(LINK "autodiff;eigen;")
    set(${current_target}_srcs ${CPPNAME})
    setup_exe_target()
endforeach()
