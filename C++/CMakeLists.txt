cmake_minimum_required(VERSION 3.25)

project(c_template)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(EXAMPLES_PATH examples)
set(SRC_PATH src)
set(INCLUDE_PATH include)
set(TEST_PATH test)
set(CMAKE_CXX_STANDARD 23)

include_directories(${INCLUDE_PATH})
include_directories(${THIRD_PARTY})
file(GLOB source_files ${SRC_PATH}/*.cpp)
add_library(${PROJECT_NAME} ${source_files})

file(GLOB examples ${EXAMPLES_PATH}/*)
foreach(example ${examples})
  get_filename_component(example_name ${example} NAME_WE)
  message("Building: ${example}")
  file(GLOB sources ${example}/*.cpp)
  add_executable(${example_name} ${sources})
  target_link_libraries(${example_name} ${PROJECT_NAME})
endforeach()

file(GLOB test_files ${TEST_PATH}/*.cpp)

add_executable(run_tests ${test_files})
target_link_libraries(run_tests ${PROJECT_NAME})
