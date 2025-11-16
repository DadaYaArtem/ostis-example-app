file(GLOB_RECURSE SOURCES CONFIGURE_DEPENDS
    "*.hpp" "*.cpp"
)

# Exclude test files from the main module
list(FILTER SOURCES EXCLUDE REGEX ".*/test/.*")

add_library(example-module SHARED ${SOURCES})
target_link_libraries(example-module
    LINK_PUBLIC sc-machine::sc-memory
    LINK_PUBLIC sc-machine::sc-agents-common
    LINK_PUBLIC scl-machine::inference
)
target_include_directories(example-module
    PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}
)
set_target_properties(example-module PROPERTIES LIBRARY_OUTPUT_DIRECTORY ${SC_EXTENSIONS_DIRECTORY})

if(${SC_CLANG_FORMAT_CODE})
    target_clangformat_setup(example-module)
endif()

if(${SC_BUILD_TESTS})
    add_subdirectory(test)
endif()
