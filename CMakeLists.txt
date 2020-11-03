cmake_minimum_required(VERSION 3.17 FATAL_ERROR)

project(qtConsole LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

enable_testing()
#add_subdirectory(googletest) #https://www.eriksmistad.no/getting-started-with-google-test-on-ubuntu/

# find_package(Python2 COMPONENTS Interpreter Development)
find_package(Python3 COMPONENTS Interpreter Development NumPy)

# https://cmake.org/cmake/help/latest/manual/cmake-qt.7.html
find_package(Qt5 COMPONENTS Core Widgets REQUIRED)

#Prevents Keywords being overwritten between Qt and Python C++ API.
ADD_DEFINITIONS(-DQT_NO_KEYWORDS)

set(Headers
  include/qconsole.h
  include/qpyconsole.h
)
set(Sources
  src/pymain.cpp
  src/qconsole.cpp
  src/qpyconsole.cpp
)

add_library(lib-qpyconsole include/qpyconsole.h src/qpyconsole.cpp)
target_link_libraries(lib-qpyconsole 
      Python3::Python
      Python3::NumPy      
      Qt5::Core
      Qt5::Widgets
)
add_library(lib-qconsole include/qconsole.h src/qconsole.cpp)
target_link_libraries(lib-qconsole 
      Qt5::Core
      Qt5::Widgets
)


include_directories(include)
add_executable(qtConsole  ${Sources} ${Headers})
target_link_libraries(qtConsole
  Python3::Python
  Python3::NumPy
  Qt5::Core
  Qt5::Widgets
)



#add_subdirectory(test)
