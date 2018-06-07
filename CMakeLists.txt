cmake_minimum_required(VERSION 2.8.3)
project(tivac_serial)

## Compile as C++11, supported in ROS Kinetic and newer
# add_compile_options(-std=c++11)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  message_generation
  rosserial_client
  rosserial_tivac
  std_msgs
)

catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES tivac_serial
#  CATKIN_DEPENDS rosserial_client rosserial_tivac std_msgs
#  DEPENDS system_lib
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
include_directories(
# include
  ${catkin_INCLUDE_DIRS}
)

rosserial_generate_ros_lib(
  PACKAGE rosserial_tivac
  SCRIPT make_libraries_tiva
)

# Chatter tutorial
rosserial_configure_client(
  DIRECTORY chatter
  TOOLCHAIN_FILE ${ROSSERIAL_TIVAC_TOOLCHAIN}
)
rosserial_add_client_target(chatter chatter.axf ALL)
rosserial_add_client_target(chatter flash)
rosserial_add_client_target(chatter size)
rosserial_add_client_target(chatter dump)


rosserial_configure_client(
  DIRECTORY ionode
  TOOLCHAIN_FILE ${ROSSERIAL_TIVAC_TOOLCHAIN}
)
rosserial_add_client_target(ionode ionode.axf ALL)
rosserial_add_client_target(ionode flash)
rosserial_add_client_target(ionode size)
rosserial_add_client_target(ionode dump)

