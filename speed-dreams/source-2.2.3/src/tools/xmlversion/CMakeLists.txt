INCLUDE(../../../cmake/macros.cmake)
PROJECT(xmlversion)

SET(XMLVERSION_SOURCES main.cpp)

ADD_SDLIB_INCLUDEDIR(tgf portability)

IF (COMMAND cmake_policy)
	cmake_policy(SET CMP0003 NEW)
ENDIF(COMMAND cmake_policy)

SD_ADD_EXECUTABLE(xmlversion ${XMLVERSION_SOURCES})

IF(CMAKE_SKIP_RPATH OR CMAKE_SKIP_BUILD_RPATH)
	#WARNING: the order of the library in the line below matters! First tgf, then txml!!!
	ADD_SDLIB_LIBRARY(xmlversion portability tgf txml STATIC)
	IF(OPTION_SDL2)
	ADD_SDL2_LIBRARY(xmlversion)
ELSE(OPTION_SDL2)
	ADD_SDL_LIBRARY(xmlversion)
ENDIF(OPTION_SDL2)
ELSE(CMAKE_SKIP_RPATH OR CMAKE_SKIP_BUILD_RPATH)
	ADD_SDLIB_LIBRARY(xmlversion portability tgf txml)
ENDIF(CMAKE_SKIP_RPATH OR CMAKE_SKIP_BUILD_RPATH)

ADD_DL_LIBRARY(xmlversion)

# Note: we don't install xmlversion, as it's a only a build-time tool.
