cmake_minimum_required(VERSION 3.16 FATAL_ERROR)

project(qtConsole LANGUAGES CXX)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

option(Testing_enabled "Build testing" OFF)

# find_package(Python2 COMPONENTS Interpreter Development)
find_package(Python3 COMPONENTS Interpreter Development NumPy REQUIRED)

# https://cmake.org/cmake/help/latest/manual/cmake-qt.7.html
find_package(Qt5 COMPONENTS Core Widgets REQUIRED)

#Prevents Keywords being overwritten between Qt and Python C++ API.
ADD_DEFINITIONS(-DQT_NO_KEYWORDS)

set(Headers
  include/mainwindow.h
  include/qconsole.h
  include/qpyconsole.h
)
set(Sources
  src/pymain.cpp
  src/mainwindow.cpp
  src/qconsole.cpp
  src/qpyconsole.cpp
)

add_library(lib-qpyconsole 
  include/qconsole.h src/qconsole.cpp
  include/qpyconsole.h src/qpyconsole.cpp
)
target_include_directories(lib-qpyconsole PUBLIC include)
target_link_libraries(lib-qpyconsole 
      Python3::Python
      Python3::NumPy      
      Qt5::Core
      Qt5::Widgets
)

add_library(lib-qconsole include/qconsole.h src/qconsole.cpp)
target_include_directories(lib-qconsole PUBLIC include)
target_link_libraries(lib-qconsole 
      Qt5::Core
      Qt5::Widgets
)


add_executable(qtpyConsole  ${Sources} ${Headers})
target_include_directories(qtpyConsole PRIVATE include)
target_link_libraries(qtpyConsole
  Python3::Python
  Python3::NumPy
  Qt5::Core
  Qt5::Widgets
)

if(Testing_enabled)
  enable_testing()
  #add_subdirectory(googletest) #https://www.eriksmistad.no/getting-started-with-google-test-on-ubuntu/
  add_subdirectory(test)
endif()

