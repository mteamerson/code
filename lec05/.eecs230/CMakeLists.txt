enable_testing()

include_directories(.eecs230/include)

macro (add_cxx_flag flag)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -${flag}")
endmacro (add_cxx_flag)

include(CheckCXXCompilerFlag)
macro (safe_add_cxx_flag flag)
    check_cxx_compiler_flag(-${flag} HAS_${flag})
    if (HAS_${flag})
        add_cxx_flag(${flag})
    endif()
endmacro (safe_add_cxx_flag)

safe_add_cxx_flag(O0)
safe_add_cxx_flag(g)

macro (add_program name)
    add_executable(${name} ${ARGN})
    set_property(TARGET ${name} PROPERTY CXX_STANDARD 11)
    set_property(TARGET ${name} PROPERTY CXX_STANDARD_REQUIRED On)
endmacro (add_program)

