cmake_minimum_required(VERSION 3.28.3)
set(PROJECT_VERSION_MAJOR 0)
set(PROJECT_VERSION_MINOR 0)
set(PROJECT_VERSION_PATCH 1)
project(r_db VERSION ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}.${PROJECT_VERSION_PATCH})

include(r_build.txt)
include(FetchContent)

FetchContent_Declare(
    r_utils
    GIT_REPOSITORY https://github.com/you/r_utils.git
    FIND_PACKAGE_ARGS NAMES r_utils
)
FetchContent_MakeAvailable(r_utils)

add_library(
    r_db
    include/r_db/r_sqlite_conn.h
    source/r_sqlite_conn.cpp
    include/r_db/r_sqlite_pager.h
    source/r_sqlite_pager.cpp
    include/sqlite3/sqlite3.h
    source/sqlite3.c
)

target_include_directories(
    r_db PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

target_link_libraries(
    r_db 
    r_utils
    ${CMAKE_DL_LIBS}
)

add_subdirectory(ut)

if(PROJECT_IS_TOP_LEVEL)
configure_dev_package("r_db" "A C++ SQLite wrapper.")
endif()

install(
    DIRECTORY include/sqlite3
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
    FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp"
)
