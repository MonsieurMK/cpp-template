include(FetchContent)

FetchContent_Declare(
  googletest
  GIT_REPOSITORY https://github.com/google/googletest.git
  GIT_TAG        v1.17.0
)

# Do not install GTest alongside the project
set(INSTALL_GTEST OFF)

FetchContent_MakeAvailable(googletest)

enable_testing()

add_executable(${PROJECT_NAME}_tests)

target_sources(${PROJECT_NAME}_tests PRIVATE $<TARGET_OBJECTS:domain_tests>)

target_link_libraries(${PROJECT_NAME}_tests
PRIVATE
    GTest::gtest_main
PUBLIC
)

include(GoogleTest)
gtest_discover_tests(${PROJECT_NAME}_tests)
