file(GLOB_RECURSE SOURCES CONFIGURE_DEPENDS
    "*.hpp" "*.cpp"
)

add_library(weather-module SHARED ${SOURCES})
target_link_libraries(weather-module
    LINK_PUBLIC sc-machine::sc-memory
    LINK_PUBLIC sc-machine::sc-agents-common
)
target_include_directories(weather-module
    PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}
)
set_target_properties(weather-module PROPERTIES LIBRARY_OUTPUT_DIRECTORY ${SC_EXTENSIONS_DIRECTORY})

if(${SC_CLANG_FORMAT_CODE})
    target_clangformat_setup(weather-module)
endif()
