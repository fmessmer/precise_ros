
cmake_minimum_required(VERSION 3.0.2)
project(precise_description)

find_package(catkin REQUIRED)

catkin_package()

install(DIRECTORY config launch meshes robots urdf
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

set(robot_list
  PF400_long
  PF400_short
)

if(CATKIN_ENABLE_TESTING)
    find_package(roslaunch REQUIRED)
    foreach(robot ${robot_list})
        message("Testing robot: ${robot}")
        roslaunch_add_file_check(launch/display_robot.launch robot:=${robot})
        roslaunch_add_file_check(launch/upload_robot.launch robot:=${robot})
    endforeach()
endif()
