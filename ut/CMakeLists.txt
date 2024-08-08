
add_executable(
    r_db_ut
    include/framework.h
    source/framework.cpp
    include/test_r_db.h
    source/test_r_db.cpp
)

if(MSVC)
    target_link_options(r_db_ut PUBLIC "/STACK:10000000")
endif()

target_include_directories(
    r_db_ut PUBLIC 
    include
    ../include
)
target_link_libraries(
    r_db_ut LINK_PUBLIC 
    r_db
    r_utils
)
if(CMAKE_SYSTEM MATCHES "Linux-")
    target_link_libraries(
        r_db_ut PUBLIC
        pthread
        dl
        uuid
    )
elseif(CMAKE_SYSTEM MATCHES "Windows")
endif(CMAKE_SYSTEM MATCHES "Linux-")
