################################################################################
# This is the CMakeLists file for your Ophidian project..
#
#   Here is your playground feel free to add your compilation targets. 
################################################################################

# Recursively fetch test code
file(GLOB_RECURSE tests_SRC  
    "*.cpp"
)

# Add test target
#add_executable(ophidian_project_tests ${tests_SRC})
