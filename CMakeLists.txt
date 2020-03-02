project( template_test_seams )
cmake_minimum_required( VERSION 3.8 )

if( MSVC )
    add_compile_options( /W3 /WX )
else()
    add_compile_options( -Wall -Wextra -pedantic -mtune=native -march=native )
endif()

add_executable( main
    src/main.cpp
    src/hello_world.cpp
)
#target_link_libraries( main Threads::Threads )
target_include_directories( main PRIVATE src )
target_compile_features( main PUBLIC cxx_std_17 )

add_executable( test_file
    src/test_file.cpp
)
#target_link_libraries( test_file Threads::Threads )
target_compile_features( test_file PUBLIC cxx_std_17 )
#target_include_directories( test_file PRIVATE include )
