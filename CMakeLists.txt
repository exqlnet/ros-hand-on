cmake_minimum_required(VERSION 2.8.3)
project(ros_tutorials_topic)


# 如果这些包不存在，在构建时会发生错误
find_package(catkin REQUIRED COMPONENTS
  message_generation
  roscpp
  std_msgs
)

# 设置消息文件
add_message_files(
  FILES
  MsgTutorial.msg
)

## Generate added messages and services with any dependencies listed here
## 设置消息依赖性
generate_messages(
  DEPENDENCIES
  std_msgs
)


# catkin功能包
catkin_package(
  LIBRARIES ros_tutorials_topic
  CATKIN_DEPENDS std_msgs roscpp
)

# 设置包含根目录
include_directories(
  ${catkin_INCLUDE_DIRS}
)

# 发布者
add_executable(topic_publisher src/topic_publisher.cpp)
add_dependencies(topic_publisher ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(topic_publisher ${catkin_LIBRARIES})

# 订阅者
add_executable(topic_subscriber src/topic_subscriber.cpp)
add_dependencies(topic_subscriber ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(topic_subscriber ${catkin_LIBRARIES})

