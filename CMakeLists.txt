cmake_minimum_required(VERSION 3.2)

project(asampl)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_FLAGS "-Wall -Wno-sign-compare -g")

add_subdirectory(deps/dynalo EXCLUDE_FROM_ALL)
add_subdirectory(deps/asampl-ffi)

add_library(asampl-interface INTERFACE)
target_include_directories(asampl-interface INTERFACE include)

add_subdirectory(src)

# executable
add_executable(asampl Asampl.cpp)

target_link_libraries(asampl asampl-lib asampl-ffi)

#handlers
file(GLOB HANDLERS handlers/*)
foreach(HANDLER_DIR ${HANDLERS})
    add_subdirectory(${HANDLER_DIR})
endforeach()

install(TARGETS asampl RUNTIME DESTINATION bin)
