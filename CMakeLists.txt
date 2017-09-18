################################################################################
# This is the main CMakeLists file for creation a Ophidian project. 
#
# Its main goals are:
#   - set up global variables.
#   - set up the global include directories
#   - add subdirectories
################################################################################

# Set up minimal cmake version
cmake_minimum_required(VERSION 3.2.2)

# Here you need to set your project name
set(PROJECT_NAME "OPHIDIAN_PROJECT_TEMPLATE")
project(${PROJECT_NAME})

# Subproject uses c++ 14
set(CMAKE_CXX_STANDARD 14)

# Fetch Ophidian
execute_process(
    COMMAND git submodule update --init --recursive
    WORKING_DIRECTORY ${PROJECT_SOURCE_DIR}
    RESULT_VARIABLE submodule_init_exit_code
)

# Configure Ophidian variables
set(OPHIDIAN_SOURCE_DIR ${PROJECT_SOURCE_DIR}/ophidian)
set(OPHIDIAN_BINARY_DIR ${PROJECT_BINARY_DIR}/ophidian)
set(OPHIDIAN_INCLUDE_DIRECTORIES 
    ${OPHIDIAN_SOURCE_DIR}
    ${OPHIDIAN_SOURCE_DIR}/3rdparty
    ${OPHIDIAN_BINARY_DIR}/3rdparty/Lemon/
    ${OPHIDIAN_SOURCE_DIR}/3rdparty/Lemon/
    ${OPHIDIAN_BINARY_DIR}/3rdparty/Lemon/lemon
)

# Set Ophidian include paths
include_directories(${OPHIDIAN_INCLUDE_DIRECTORIES})

# Set project include path 
include_directories(src)

# Add ophidian sibdirectory
add_subdirectory(${OPHIDIAN_SOURCE_DIR})

# Then add project source subdirectory
add_subdirectory(src)

# Then add project test subdirectory
add_subdirectory(test)
