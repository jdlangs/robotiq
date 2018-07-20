cmake_minimum_required(VERSION 2.8.3)
project(robotiq_ethercat)

find_package(catkin REQUIRED COMPONENTS
  roscpp
)

#set(soem_ROOT_DIR $ENV{HOME}/Software/SOEM)
#set(soem_INCLUDE_DIRS
#${soem_ROOT_DIR}
#${soem_ROOT_DIR}/osal
#${soem_ROOT_DIR}/osal/linux
#${soem_ROOT_DIR}/oshw
#)
find_library(SOEM soem PATHS /usr/local)

catkin_package(
   INCLUDE_DIRS include
   LIBRARIES robotiq_ethercat
   CATKIN_DEPENDS roscpp
)

include_directories(include
  ${catkin_INCLUDE_DIRS}
  #${soem_INCLUDE_DIRS}
)

add_library(robotiq_ethercat
 include/robotiq_ethercat/ethercat_manager.h
 src/ethercat_manager.cpp
)

target_link_libraries(robotiq_ethercat
  ${SOEM}
)

install(TARGETS robotiq_ethercat
   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
 )

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h"
)
