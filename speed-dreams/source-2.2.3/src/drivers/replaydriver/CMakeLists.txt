# This program has been developed by students from the bachelor Computer Science at
# Utrecht University within the Software Project course.
# © Copyright Utrecht University (Department of Information and Computing Sciences)

INCLUDE(../../../cmake/macros.cmake)

SET(ROBOT_NAME "replaydriver")
SET(ROBOT_INTERFACE WELCOME)
SET(ROBOT_SOURCES ${ROBOT_NAME}.cpp Driver.cpp Driver.h)

ADD_SDLIB_INCLUDEDIR(robottools tgfclient backend rppUtils)

ROBOT_MODULE(NAME ${ROBOT_NAME} VERSION 1.0.0 SOVERSION 1.0.0
             INTERFACE ${ROBOT_INTERFACE}
             SOURCES ${ROBOT_SOURCES})

ADD_SDLIB_LIBRARY(${ROBOT_NAME} robottools tgfclient backend)

# For data associated to the robot module, see data/drivers/replaydriver/CMakeLists.txt
