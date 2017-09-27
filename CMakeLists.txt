################################################################################
# This is the main CMakeLists file for creation a Ophidian project. 
#
# Its main goals are:
#   - set up global variables.
#   - set up the global include directories
#   - add subdirectories
################################################################################

################################################################################
# Set up global variables
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

# Set Ophidian paths
set(OPHIDIAN_SOURCE_DIR ${PROJECT_SOURCE_DIR}/ophidian)
set(OPHIDIAN_BINARY_DIR ${PROJECT_BINARY_DIR}/ophidian)

# Set Ophidian Dependencies path
set(OPHIDIAN_DEPENDENCIES_DIR ${OPHIDIAN_SOURCE_DIR}/3rdparty)

# Set Lemon include paths
set(LEMON_INCLUDE_DIR 
    ${OPHIDIAN_SOURCE_DIR}/3rdparty/Lemon/
    ${OPHIDIAN_BINARY_DIR}/3rdparty/Lemon/
    ${OPHIDIAN_BINARY_DIR}/3rdparty/Lemon/lemon
)

################################################################################
# Project logic 
################################################################################

# Configure project include paths
include_directories(
    ${PROJECT_SOURCE_DIR}/src

    ${OPHIDIAN_SOURCE_DIR}
    ${OPHIDIAN_DEPENDENCIES_DIR}
    ${LEMON_INCLUDE_DIR}
)

# Set option build shared libs
option(BUILD_SHARED_LIBS "on/off -> (build every non statc lib shared)/(build everything static)" ON)

# Add ophidian subdirectory
add_subdirectory(${OPHIDIAN_SOURCE_DIR})

# Then add project source subdirectory
add_subdirectory(src)

# Then add project test subdirectory
add_subdirectory(test)
