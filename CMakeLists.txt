cmake_minimum_required(VERSION 3.10)

project(kakoune)

#set(CURSES_NEED_NCURSES TRUE)
find_package(Curses REQUIRED)
include_directories(${CURSES_INCLUDE_DIRS})

set(KAKOUNE_VERSION "unknown")

configure_file (
  "${CMAKE_SOURCE_DIR}/src/version.cc.in"
  "${CMAKE_SOURCE_DIR}/src/version.cc"
)

set(CMAKE_CXX_STANDARD 14)

set(CMAKE_CXX_FLAGS "-D'KAK_BIN_PATH=\"/usr/local/bin/kak\"'")
#set(CMAKE_EXE_LINKER_FLAGS "-L/usr/local/lib -lncursesw")

LINK_DIRECTORIES(/usr/local/lib)

#target_compile_options(-Wall)
#target_link_libraries()

file(GLOB_RECURSE SOURCES RELATIVE ${CMAKE_SOURCE_DIR} "src/*.cc")
add_executable(kak ${SOURCES})
target_link_libraries(kak ${CURSES_LIBRARIES})

