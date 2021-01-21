file (GLOB HEADERS "*.h")
file (GLOB SOURCES "[^_]*.cc")

add_library(mve STATIC ${SOURCES} ${HEADERS})
target_include_directories(mve PRIVATE ${JPEG_INCLUDE_DIR})


if(CMAKE_CXX_COMPILER_ID STREQUAL "MSVC")
target_link_libraries(mve
    PUBLIC
        mve_math
        mve_util
    PRIVATE
        JPEG::JPEG
        PNG::PNG
        TIFF::TIFF
)
else()
target_link_libraries(mve
    PUBLIC
        mve_math
        mve_util
    PRIVATE
        jpeg
        PNG::PNG
        TIFF::TIFF
)
endif()
