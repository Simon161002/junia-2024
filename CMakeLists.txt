cmake_minimum_required(VERSION 3.14)

project(walle-app LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# La target ici est walle-lib
add_library(walle-lib SHARED
            src/walle-lib/environment.cpp
            src/walle-lib/environment.hpp
            src/walle-lib/element.cpp
            src/walle-lib/element.hpp
            src/walle-lib/robot.cpp
            src/walle-lib/robot.hpp
            src/walle-lib/planting_robot.cpp
            src/walle-lib/planting_robot.hpp
            src/walle-lib/tree.hpp
            src/walle-lib/obstacle.hpp
            src/walle-lib/vector2.cpp
            src/walle-lib/vector2.hpp)
            
target_include_directories(walle-lib
  PUBLIC
  ${CMAKE_CURRENT_SOURCE_DIR}/src/
)

add_executable(walle-app
               src/walle-app/main.cpp
             )

target_link_libraries(walle-app
                      walle-lib)

install(
    TARGETS walle-app
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})

add_subdirectory(tests)

add_executable(all-tests
  tests/src/test_environment.cpp
  tests/src/test_element.cpp
  tests/src/test_robot.cpp
  tests/src/test_vector2.cpp  
  tests/src/test_planting_robot.cpp
)

target_link_libraries(
  all-tests
  walle-lib
  GTest::gtest_main
)
