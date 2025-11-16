# Test utilities library
file(GLOB TEST_UTILS_SOURCES CONFIGURE_DEPENDS
    "utils/*.hpp"
    "utils/*.cpp"
)

add_library(example-module-test-utils STATIC ${TEST_UTILS_SOURCES})
target_link_libraries(example-module-test-utils
    LINK_PUBLIC sc-machine::sc-memory
    LINK_PUBLIC GTest::gtest
)
target_include_directories(example-module-test-utils
    PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}
)

# Test executable
file(GLOB TEST_SOURCES CONFIGURE_DEPENDS
    "units/*.cpp"
)

add_executable(example-module-tests ${TEST_SOURCES})
target_link_libraries(example-module-tests
    LINK_PUBLIC example-module-test-utils
    LINK_PUBLIC sc-machine::sc-memory
    LINK_PUBLIC sc-machine::sc-agents-common
    LINK_PUBLIC scl-machine::inference
    LINK_PUBLIC GTest::gtest_main
)
target_include_directories(example-module-tests
    PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/..
)

# Copy test structures to build directory
file(COPY ${CMAKE_CURRENT_SOURCE_DIR}/test-structures
     DESTINATION ${CMAKE_CURRENT_BINARY_DIR})

gtest_discover_tests(example-module-tests)
