# RoboComp global CMake
cmake_minimum_required(VERSION 3.12)
project(RoboComp)
#string(TOLOWER ${PROJECT_NAME} PROJECT_NAME_LOWER)
set(RoboComp_INTERFACES_DIR ${RoboComp_SOURCE_DIR}/interfaces)

add_subdirectory(libs)
add_subdirectory(tools)


# Install rules necessary to allow compiling components without the robocomp's source code
#INSTALL(FILES "files/robocomp.conf" DESTINATION /etc/ld.so.conf.d/)
#INSTALL(DIRECTORY "interfaces" DESTINATION /opt/robocomp/ )
#INSTALL(DIRECTORY "cmake" DESTINATION /opt/robocomp/ )
##INSTALL(DIRECTORY "files" DESTINATION /opt/robocomp/ )
#INSTALL(DIRECTORY "classes" DESTINATION /opt/robocomp/ )
