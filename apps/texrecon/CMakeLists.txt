file (GLOB HEADERS "*.h")
file (GLOB SOURCES "[^_]*.cpp")

set(BIN texrecon)

add_executable(${BIN} ${SOURCES})
set_property(TARGET ${BIN} PROPERTY INTERPROCEDURAL_OPTIMIZATION True)

target_link_libraries(${BIN} tex ${TBB_LIBRARIES} mve mve_util mve_math)
install(TARGETS ${BIN} RUNTIME DESTINATION bin)
