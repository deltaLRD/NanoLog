cmake_minimum_required(VERSION 3.14)

project(NANOLOG)

set(CXX_STANDARD 17 REQUIRED)
set(RUNTIME_DIR ${PROJECT_SOURCE_DIR}/runtime)
set(SAMPLE_BUILD bool)
set(SAMPLE_PREPROCESSOR_BUILD bool)
set(INTEGRATION_TEST_BUILD bool)

# Common Sources
# SRCS=Cycles.cc Util.cc Log.cc NanoLog.cc RuntimeLogger.cc TimeTrace.cc
set(RUNTIME_COMMON_SOURCE_FILES 
    ${RUNTIME_DIR}/Cycles.cc
    ${RUNTIME_DIR}/Util.cc
    ${RUNTIME_DIR}/Log.cc
    ${RUNTIME_DIR}/NanoLog.cc
    ${RUNTIME_DIR}/RuntimeLogger.cc
    ${RUNTIME_DIR}/TimeTrace.cc
)

include_directories(${RUNTIME_DIR})


## gtest

include(FetchContent)
FetchContent_Declare(
  googletest
  # Specify the commit you depend on and update it regularly.
  URL https://github.com/google/googletest/archive/5376968f6948923e2411081fd9372e71a59d8e77.zip
)
# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

# Now simply link against gtest or gtest_main as needed. Eg
# add_executable(example example.cpp)
# target_link_libraries(example gtest_main)
# add_test(NAME example_test COMMAND example)

## gtest end

message(STATUS "###############")
message(STATUS ${PROJECT_SOURCE_DIR})
message(STATUS "###############")

message(STATUS "###############")
message(STATUS ${RUNTIME_COMMON_SOURCE_FILES})
message(STATUS "###############")
add_library(NanoLog STATIC ${RUNTIME_COMMON_SOURCE_FILES})