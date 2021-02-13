cmake_minimum_required(VERSION 3.12)
project( rcis )
include( src/CMakeListsSpecific.txt )
INCLUDE (${CMAKE_SOURCE_DIR}/cmake/modules/qt.cmake )
#SET( CMAKE_AUTOMOC ON )
#SET( CMAKE_AUTOUIC ON )
find_package(Qt5 COMPONENTS Core Gui REQUIRED)
find_package(Ice 3.7 COMPONENTS Ice REQUIRED)
INCLUDE( ${CMAKE_SOURCE_DIR}/cmake/robocompLocal.cmake )
ROBOCOMP_IDSL_TO_ICE( Camera CommonBehavior CommonHead DifferentialRobot OmniRobot IMU InnerModelManager JointMotor Laser RGBD TouchSensor RCISMousePicker GenericBase Display)
ROBOCOMP_ICE_TO_SRC( Camera CommonBehavior CommonHead DifferentialRobot OmniRobot IMU InnerModelManager JointMotor Laser RGBD TouchSensor RCISMousePicker GenericBase Display)


add_executable(rcis )
target_sources(rcis
        PRIVATE ${SPECIFIC_SOURCES}
        src/robotsimulatorcomp.cpp
        src/genericworker.cpp
        src/genericmonitor.cpp
        src/cameraI.cpp
        src/differentialrobotI.cpp
        src/genericbaseI.cpp
        src/omnirobotI.cpp
        src/imuI.cpp
        src/innermodelmanagerI.cpp
        src/jointmotorI.cpp
        src/laserI.cpp
        src/rgbdI.cpp
        src/displayI.cpp
        src/touchsensorI.cpp
        ${CMAKE_SOURCE_DIR}/classes/rapplication/rapplication.cpp
        ${CMAKE_SOURCE_DIR}/classes/qlog/qlog.cpp)
target_link_directories(rcis PRIVATE Qt5::Gui Qt5::Core Robocomp::innermodel Robocomp::qmat Robocomp::osgviewer pthread glut OpenThreads osg osgGA osgDB osgUtil osgText boost_system boost_thread ${Ice_LIBRARIES})
target_link_libraries(rcis
        PRIVATE Qt5::Gui Qt5::Core Robocomp::innermodel Robocomp::qmat Robocomp::osgviewer pthread glut OpenThreads osg osgGA osgDB osgUtil osgText boost_system boost_thread ${Ice_LIBRARIES})
target_include_directories(rcis PRIVATE src/ ${CMAKE_SOURCE_DIR}/classes/)
target_compile_features(rcis PRIVATE cxx_std_17)

#add_custom_target(doc doxygen Doxyfile)
#add_custom_target(installdoc mkdir -p /opt/robocomp/doc COMMAND cp -R doc/html /opt/robocomp/doc/rcis )
