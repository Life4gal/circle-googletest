project(
		circle-googletest-unit-test
		LANGUAGES CXX
)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

set(
		${PROJECT_NAME}_SOURCE
		
		src/main.cpp
)

add_executable(
		${PROJECT_NAME}
		
		${${PROJECT_NAME}_SOURCE}
)

set_compile_options_private(${PROJECT_NAME})

# todo: google-test will pass a lot of compiler arguments to the compiler that gcc/clang supports, but unfortunately circle doesn't currently support them :(
include(${${PROJECT_NAME_PREFIX}CMAKE_3RDPARTY_PATH}/google-test.cmake)

target_link_libraries(
		${PROJECT_NAME}
		PRIVATE
		gtest_main
)

# for gtest_discover_tests
include(GoogleTest)
gtest_discover_tests(${PROJECT_NAME})
