cmake_minimum_required(VERSION 3.2)

project(helloworld VERSION 0.0.1)

configure_file(version.h.in version.h)

add_executable(helloworld main.cpp)
add_library(helloworldlib lib.cpp)


set_target_properties(helloworld helloworldlib PROPERTIES
    CXX_STANDARD 14
    CXX_STANDARD_REQUIRED ON
)

target_include_directories(helloworldlib
    PRIVATE "${CMAKE_BINARY_DIR}"
)

target_link_libraries(helloworld PRIVATE
    helloworldlib
)

if (MSVC)
    target_compile_options(helloworld PRIVATE
        /W4
    )
    target_compile_options(helloworldlib PRIVATE
        /W4
    )
    #target_compile_options(test_version PRIVATE
    #    /W4
    #)
else ()
    target_compile_options(helloworld PRIVATE
        -Wall -Wextra -pedantic -Werror
    )
    target_compile_options(helloworldlib PRIVATE
        -Wall -Wextra -pedantic -Werror
    )
    #target_compile_options(test_version PRIVATE
    #    -Wall -Wextra -pedantic -Werror
   # )
endif()