cmake_minimum_required(VERSION 3.5)
project(camera_driver)

SET(OpenCV_DIR /usr/local/share/OpenCV)
find_package(OpenCV REQUIRED)
find_package(catkin REQUIRED COMPONENTS
  cv_bridge
  image_transport
  message_generation
  message_runtime
  roscpp
  sensor_msgs
  std_msgs
)
find_package(PCL REQUIRED)

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

catkin_package(CATKIN_DEPENDS cv_bridge image_transport message_generation roscpp sensor_msgs std_msgs
)

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${OpenCV_INCLUDE_DIRS}
  ${PCL_INCLUDE_DIRS}
)


add_executable(image_show src/image_show.cpp)
add_dependencies(image_show ${catkin_EXPORTED_TARGETS} ${${PROJECT_NAME}_EXPORTED_TARGETS})
target_link_libraries(image_show ${catkin_LIBRARIES} ${OpenCV_LIBS})


add_executable(pcl_show src/pcl_show.cpp)
add_dependencies(pcl_show ${catkin_EXPORTED_TARGETS} ${${PROJECT_NAME}_EXPORTED_TARGETS})
target_link_libraries(pcl_show ${catkin_LIBRARIES} ${OpenCV_LIBS} ${PCL_LIBRARIES})
