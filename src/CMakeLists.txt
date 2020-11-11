file(GLOB ASAMPL_SOURCES *.cpp)

add_library(asampl-lib STATIC
    ${ASAMPL_SOURCES})

target_link_libraries(
    asampl-lib

    asampl-interface
    dynalo
    ${OpenCV_LIBRARIES})