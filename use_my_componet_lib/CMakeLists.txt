cmake_minimum_required(VERSION 3.10.0)
project(use_my_componet_lib VERSION 0.1.0 LANGUAGES CXX)

find_package(my_componet_lib REQUIRED COMPONENTS componet2 componet1)

add_executable(${PROJECT_NAME} main.cpp)
target_link_libraries(${PROJECT_NAME}
    PUBLIC
    my_componet_lib::componet2
    my_componet_lib::componet1
)
 