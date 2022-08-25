cmake_minimum_required(VERSION 3.15)

project(jpge LANGUAGES CXX)

if(NOT MSVC)
    set_property(GLOBAL PROPERTY CXX_STANDARD 11)
    
    add_compile_options(
        -Wall
        -Wextra
        -fno-strict-aliasing
    )
    
    add_compile_definitions(
        _LARGEFILE64_SOURCE=1
        _FILE_OFFSET_BITS=64
    )

    if(MINGW)
        add_compile_definitions(
            WIN32
        )
    endif()
endif()

add_library(jpgd jpgd.cpp)
target_include_directories(jpgd PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

add_library(jpge jpge.cpp)
target_include_directories(jpge PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

add_executable(tga2jpg tga2jpg.cpp timer.cpp)
target_link_libraries(tga2jpg PRIVATE jpgd jpge)

install(TARGETS jpgd jpge ARCHIVE LIBRARY)
install(TARGETS tga2jpg RUNTIME)

