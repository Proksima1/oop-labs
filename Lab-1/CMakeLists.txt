cmake_minimum_required(VERSION 3.28)
project(oop CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Werror=maybe-uninitialized")

include(FetchContent)
FetchContent_Declare(
        googletest
        GIT_REPOSITORY https://github.com/google/googletest.git
        GIT_TAG v1.15.2
        TLS_VERIFY false
)
FetchContent_MakeAvailable(googletest)
add_library(GTest::GTest INTERFACE IMPORTED)
target_link_libraries(GTest::GTest INTERFACE gtest_main)


add_executable(${CMAKE_PROJECT_NAME}_exe src/main.cpp src/program/utils.cpp)
target_include_directories(${CMAKE_PROJECT_NAME}_exe PRIVATE include)


enable_testing()
add_executable(${CMAKE_PROJECT_NAME} tests/tests.cpp src/program/utils.cpp)
target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE GTest::GTest)
target_include_directories(${CMAKE_PROJECT_NAME} PRIVATE include)


add_test(NAME ${CMAKE_PROJECT_NAME}_tests COMMAND ${CMAKE_PROJECT_NAME}_tests)