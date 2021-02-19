cmake_minimum_required(VERSION 3.5)
project(my_cpp_pkg)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(example_interfaces REQUIRED)

# Executable should not be named same as the name of the file or the name of the node
add_executable(cpp_node src/my_first_node.cpp)
# Link dependencies specific to ament
ament_target_dependencies(cpp_node rclcpp)

# Add executable to robot news station node
add_executable(robot_news_station src/robot_news_station.cpp)
ament_target_dependencies(robot_news_station rclcpp example_interfaces)

# Executable for smartphone node
add_executable(smartphone src/smartphone.cpp)
ament_target_dependencies(smartphone rclcpp example_interfaces)

# Executable for number publisher node
add_executable(number_publisher src/number_publisher.cpp)
ament_target_dependencies(number_publisher rclcpp example_interfaces)

# Executable for number counter node
add_executable(number_counter src/number_counter.cpp)
ament_target_dependencies(number_counter rclcpp example_interfaces)

install(TARGETS
    cpp_node
    robot_news_station
    smartphone
    number_publisher
    number_counter
    DESTINATION lib/${PROJECT_NAME} # Project name same as the name of th package
)

ament_package()
