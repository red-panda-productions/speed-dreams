# This program has been developed by students from the bachelor Computer Science at
# Utrecht University within the Software Project course.
# © Copyright Utrecht University (Department of Information and Computing Sciences)

INCLUDE(../../../cmake/macros.cmake)

SET(_SOURCES 
	BrakeDecision.cpp
	CarController.cpp
	DecisionMaker.cpp
	DecisionTuple.cpp
	FileDataStorage.cpp
        Decision.cpp
	InterventionExecutorAlwaysIntervene.cpp
	InterventionExecutorIndication.cpp
	InterventionExecutorNoIntervention.cpp
	InterventionExecutorAutonomousAI.cpp
	InterventionExecutorPerformWhenNeeded.cpp
	InterventionFactory.cpp
	Mediator.cpp
	Recorder.cpp
	SDAConfig.cpp
	SocketBlackBox.cpp
	SQLDatabaseStorage.cpp
	SteerDecision.cpp
	BlackBoxData.cpp
	AccelDecision.cpp
	IPCPointerManager.cpp
)

SET(_INLINES
	DecisionMaker.inl
        Mediator.inl
	SocketBlackBox.inl
	IPCPointerManager.inl)

SET(_HEADERS 
	BrakeDecision.h
	CarController.h
	ConfigEnums.h
	DecisionMaker.h
	DecisionTuple.h
	FileDataStorage.h
	IDataStorage.h
        Decision.h
	InterventionExecutor.h
	InterventionExecutorAlwaysIntervene.h
    InterventionExecutorIndication.h
	InterventionExecutorAutonomousAI.h
	InterventionExecutorNoIntervention.h
	InterventionExecutorPerformWhenNeeded.h
	InterventionFactory.h
	Mediator.h
	Recorder.h
	SDAConfig.h
	SocketBlackBox.h
	SQLDatabaseStorage.h
	SteerDecision.h
	BlackBoxData.h
	AccelDecision.h
	IPCPointerManager.h
	MySQLHeaders.h
)

ADD_INTERFACE_INCLUDEDIR()
ADD_SDLIB_INCLUDEDIR(tgf math portability frontend rppUtils unitTestUtilities)

SD_ADD_LIBRARY(backend STATIC ${_SOURCES} ${_HEADERS} ${_INLINES})

TARGET_INCLUDE_DIRECTORIES(backend PUBLIC ${CMAKE_SOURCE_DIR}/src/modules/simu/simuv4)

SET_TARGET_PROPERTIES(backend PROPERTIES LINKER_LANGUAGE CXX)

TARGET_LINK_LIBRARIES(backend frontend)

ADD_SDLIB_LIBRARY(backend tgf portability unitTestUtilities)

ADD_MSGPACK_PACKAGE(backend)

ADD_IPCLIB_PACKAGE(backend)

ADD_MYSQL_PACKAGE(backend)

ADD_BOOST_PACKAGE(backend)

IF(UNIX)
	TARGET_LINK_LIBRARIES(backend rt)
ENDIF(UNIX)

SD_INSTALL_FILES(LIB simulatedDrivingAssistance/backend TARGETS backend)