# ==============================================================
# Tests
# ==============================================================

cmake_minimum_required(VERSION 3.20)
project(HashFlatMapTest)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
include(GNUInstallDirs)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

cmake_path(GET CMAKE_CURRENT_SOURCE_DIR PARENT_PATH PARENT_DIR)

# Add a testing executable
add_executable(${PROJECT_NAME} test_main.cpp)

target_include_directories(${PROJECT_NAME} PRIVATE ${PARENT_DIR}/include)

include(${PARENT_DIR}/cmake/CompilerWarnings.cmake)
include(${PARENT_DIR}/cmake/Sanitizers.cmake)

myproject_set_project_warnings(${PROJECT_NAME} TRUE "X" "" "" "X")
myproject_enable_sanitizers(${PROJECT_NAME} TRUE TRUE TRUE FALSE FALSE)

Include(FetchContent)

FetchContent_Declare(
  Catch2
  GIT_REPOSITORY https://github.com/catchorg/Catch2.git
  GIT_TAG        v3.4.0 # or a later release
)

FetchContent_MakeAvailable(Catch2)

target_link_libraries(${PROJECT_NAME} PRIVATE Catch2::Catch2WithMain)

# we cannot analyse results without gcov
# find_program(GCOV_PATH gcov)
# if(NOT GCOV_PATH)
#   message(FATAL_ERROR "Code coverage analysis requires gcov!")
# endif()

