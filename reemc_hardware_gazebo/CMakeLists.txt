cmake_minimum_required(VERSION 2.8.3)
project(reemc_hardware_gazebo)

find_package(catkin REQUIRED
    COMPONENTS
      angles
      hardware_interface
      joint_limits_interface
      gazebo_ros_control
      control_toolbox
    )

find_package(gazebo REQUIRED)

catkin_package(
    INCLUDE_DIRS include
    CATKIN_DEPENDS
      control_toolbox
      gazebo_ros_control
      joint_limits_interface
      hardware_interface
    LIBRARIES ${PROJECT_NAME}
)

include_directories(include ${catkin_INCLUDE_DIRS} ${GAZEBO_INCLUDE_DIRS})
link_directories(${GAZEBO_LIBRARY_DIRS})

add_library(${PROJECT_NAME} src/reemc_hardware_gazebo.cpp)
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES} ${GAZEBO_LIBRARIES})

install(TARGETS ${PROJECT_NAME}
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
  )

install(DIRECTORY include/
   DESTINATION ${CATKIN_GLOBAL_INCLUDE_DESTINATION}
   FILES_MATCHING PATTERN "*.h"
)
install (FILES reemc_hardware_gazebo_plugins.xml
    DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})
