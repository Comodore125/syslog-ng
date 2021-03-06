set(CSVPARSER_SOURCES
    csvparser.c
    csvparser.h
    csvparser-parser.c
    csvparser-parser.h
    csvparser-plugin.c
    ${CMAKE_CURRENT_BINARY_DIR}/csvparser-grammar.h
    ${CMAKE_CURRENT_BINARY_DIR}/csvparser-grammar.c
)

generate_y_from_ym(modules/csvparser/csvparser-grammar)

bison_target(CSVParserGrammar
    ${CMAKE_CURRENT_BINARY_DIR}/csvparser-grammar.y
    ${CMAKE_CURRENT_BINARY_DIR}/csvparser-grammar.c
    COMPILE_FLAGS ${BISON_FLAGS})

include_directories (${CMAKE_CURRENT_BINARY_DIR})
include_directories (${CMAKE_CURRENT_SOURCE_DIR})
add_library(csvparser MODULE ${CSVPARSER_SOURCES})
target_link_libraries(csvparser PRIVATE syslog-ng)

install(TARGETS csvparser LIBRARY DESTINATION lib/syslog-ng/ COMPONENT csvparser)
