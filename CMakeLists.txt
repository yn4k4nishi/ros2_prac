cmake_minimum_required(VERSION 3.5)
project(ros2_prac)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
find_package(example_interfaces REQUIRED)
find_package(action_tutorials_interfaces REQUIRED)

add_executable(talker src/talker.cpp)
ament_target_dependencies(talker rclcpp std_msgs)

add_executable(listener src/listener.cpp)
ament_target_dependencies(listener rclcpp std_msgs)

add_executable(server src/server.cpp)
ament_target_dependencies(server rclcpp std_msgs example_interfaces)

add_executable(client src/client.cpp)
ament_target_dependencies(client rclcpp std_msgs example_interfaces)

add_executable(action_server src/action_server.cpp)
ament_target_dependencies(action_server rclcpp std_msgs action_tutorials_interfaces)

install(TARGETS
        talker
        listener
        server
        client
        DESTINATION lib/${PROJECT_NAME}
        )

ament_package()
