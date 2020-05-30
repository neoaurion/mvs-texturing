file (GLOB HEADERS "*.h")
file (GLOB SOURCES "[^_]*.cc")

add_library(mve_acc STATIC ${SOURCES} ${HEADERS})

