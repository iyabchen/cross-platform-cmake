CMAKE_MINIMUM_REQUIRED (VERSION 3.4)
project(app)
if (WIN32)
    set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)
endif()

add_library(sum SHARED sum.cpp sum.h )
add_library(addten SHARED addten.cpp addten.h)
target_link_libraries(addten PRIVATE sum)
