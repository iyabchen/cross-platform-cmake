CMAKE_MINIMUM_REQUIRED (VERSION 3.4)
project(main)
if (WIN32)
    set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)
endif()

add_executable(main main.cpp "${CMAKE_CURRENT_SOURCE_DIR}/../app/sum.h")

find_library(sumlib sum "${CMAKE_CURRENT_SOURCE_DIR}/../app/build/Debug")
message(status "${sumlib}")
find_library(addtenlib addten "${CMAKE_CURRENT_SOURCE_DIR}/../app/build/Debug")
message(status "${addtenlib}")
target_link_libraries(main ${sumlib} ${addtenlib} )