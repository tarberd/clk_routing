file(GLOB_RECURSE tests_SRC  
    "*.cpp"
)

add_executable(tests ${tests_SRC})
target_link_libraries(tests PUBLIC 
    Catch 
    lemon
)
