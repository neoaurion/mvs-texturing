file (GLOB HEADERS "*.h")
file (GLOB SOURCES "[^_]*.cpp")

set(LIBRARY tex)
add_library(${LIBRARY} STATIC ${SOURCES})
set_property(TARGET ${LIBRARY} PROPERTY INTERPROCEDURAL_OPTIMIZATION True)
#add_dependencies(${LIBRARY} ext_mapmap)
target_link_libraries(${LIBRARY} ${TBB_LIBRARIES} mve mve_util mve_math ${JPEG_LIBRARIES} ${PNG_LIBRARIES} ${TIFF_LIBRARIES} Eigen3::Eigen TBB::tbb)
install(TARGETS ${LIBRARY} ARCHIVE DESTINATION lib)
