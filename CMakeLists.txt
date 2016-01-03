cmake_minimum_required(VERSION 2.8.3)
project(teensy_test)

find_package(catkin REQUIRED COMPONENTS
    ros_teensy
    rosserial_client
    rosserial_arduino
    std_msgs
    message_generation
)

add_service_files(FILES
    ToggleLed.srv
)

generate_messages()

rosserial_generate_ros_lib(
    PACKAGE rosserial_arduino
    SCRIPT make_libraries.py
)

rosserial_configure_client(
    DIRECTORY drive
    TOOLCHAIN_FILE ${ROS_TEENSY_TOOLCHAIN}
)

rosserial_configure_client(
    DIRECTORY blink
    TOOLCHAIN_FILE ${ROS_TEENSY_TOOLCHAIN}
)

rosserial_add_client_target(drive driver_Firmware ALL)
rosserial_add_client_target(blink toggle_Firmware ALL)

