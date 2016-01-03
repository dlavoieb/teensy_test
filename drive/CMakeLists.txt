cmake_minimum_required(VERSION 2.8.3)

import_arduino_library(Servo)
import_arduino_library(SPI)

include_directories(${ROS_LIB_DIR})

## Build the ros_lib directory as a library we can link to
FILE(GLOB_RECURSE ros_src 
    "${ROS_LIB_DIR}/*.c" 
    "${ROS_LIB_DIR}/*.cpp" 
    "${ROS_LIB_DIR}/*.h")
add_library(ros_lib ${ros_src})

## build the executables and link to ros libraries
add_teensy_executable(driver Drive.cpp)
target_link_libraries(driver ros_lib)
