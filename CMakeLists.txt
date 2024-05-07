cmake_minimum_required(VERSION 3.5)
project(trompeloeil-effcpp VERSION 0.0.1 LANGUAGES CXX)

include(FetchContent)

# doctest
FetchContent_Declare(
    doctest
    GIT_REPOSITORY https://github.com/doctest/doctest.git
    # corresponds to doctest v2.4.11
    GIT_TAG "ae7a13539fb71f270b87eb2e874fbac80bc8dda2" )

# trompeloeil
FetchContent_Declare(
    trompeloeil
    GIT_REPOSITORY https://github.com/rollbear/trompeloeil.git
    # corresponds to trompeloeil v47
    GIT_TAG "ad9bc41b1e01ae92802de59a12d19cf7c8683d6d" )

# make the dependencies available to the build system
FetchContent_MakeAvailable(doctest trompeloeil)

set(testname ${PROJECT_NAME}-test)
add_executable(${testname} main.cpp)
target_compile_features(${testname} PRIVATE cxx_std_17)
target_link_libraries(${testname} PUBLIC doctest::doctest trompeloeil::trompeloeil)

target_sources(
  ${testname}
  PRIVATE
    # ${NWOT_PATH}/unittest_mocks/mosquittopp_loopback/mosquittopp_loopback_mock.cc
    # ${CMAKE_SOURCE_DIR}/src/DupManager.cpp
    test.cpp
    )

target_compile_options(${testname} PRIVATE
    -pedantic-errors
    -Wall
    -Weffc++
)
