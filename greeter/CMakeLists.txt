cmake_minimum_required(VERSION 3.10)
project(greter1)

#Ustawienie wersji kompilatora ver1
#set(CMAKE_CXX_STANDARD 17)
#set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(SRC 
    greeter.cpp 
    person.cpp)

set(FLAGS PRIVATE -Wall -Wextra -Werror -pedantic -Wconversion -O3)

                      
add_library(${PROJECT_NAME}-lib STATIC ${SRC})
target_compile_options(${PROJECT_NAME}-lib ${FLAGS})
target_compile_features(${PROJECT_NAME}-lib PRIVATE cxx_std_17)

add_executable(${PROJECT_NAME} main.cpp)
target_compile_options(${PROJECT_NAME} ${FLAGS})
target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_17)

add_executable(${PROJECT_NAME}-ut test/greeter.ut.cpp)
target_compile_options(${PROJECT_NAME}-ut ${FLAGS})
target_compile_features(${PROJECT_NAME}-ut PRIVATE cxx_std_17)


target_link_libraries(${PROJECT_NAME} ${PROJECT_NAME}-lib)
target_link_libraries(${PROJECT_NAME}-ut ${PROJECT_NAME}-lib) 

#Ustawienie wersji kompilatora ver3
#set_target_properties(${PROJECT_NAME}-lib PROPERTIES
#                      CXX_STANDARD 17
#                      CXX_STANDARD_REQUIRED ON)
#set_target_properties(${PROJECT_NAME} PROPERTIES
#                      CXX_STANDARD 17
#                      CXX_STANDARD_REQUIRED ON)
#set_target_properties(${PROJECT_NAME}-ut PROPERTIES
#                      CXX_STANDARD 17
#                      CXX_STANDARD_REQUIRED ON)

enable_testing()
add_test(NAME MyTest COMMAND ${PROJECT_NAME}-ut)
