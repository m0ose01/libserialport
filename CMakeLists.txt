cmake_minimum_required(VERSION 4.1.2)

project(libserialport)

set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_STANDARD 99)

set(CMAKE_SHARED_LIBRARY_PREFIX "")
set(CMAKE_STATIC_LIBRARY_PREFIX "")

add_library(${PROJECT_NAME} STATIC)

target_sources(${PROJECT_NAME} PRIVATE
	"serialport.c"
	"timing.c"
	"libserialport_internal.h"
)

target_compile_definitions(${PROJECT_NAME} PRIVATE
	SP_PRIV="do{}while(0)"
	USING_CMAKE
)

target_include_directories(${PROJECT_NAME} PUBLIC
	${CMAKE_CURRENT_SOURCE_DIR}
)

if(LINUX)
	message(FATAL_ERROR "WIN32 not yet supported.")

	target_sources(${PROJECT_NAME} PRIVATE
		"linux.c"
		"linux_termios.c"
		"linux_termios.h"
	)

endif(LINUX)

if (APPLE)
	target_sources(${PROJECT_NAME} PRIVATE
		"macosx.c"
	)

	target_link_options(${PROJECT_NAME} PUBLIC
		"SHELL: -framework IOKit"
		"SHELL: -framework CoreFoundation"
	)

endif(APPLE)

if(WIN32)

	target_sources(${PROJECT_NAME} PRIVATE
		"windows.c"
	)

	target_compile_definitions(${PROJECT_NAME} PRIVATE
		LIBSERIALPORT_MSBUILD
	)

	target_link_libraries(libserialport INTERFACE setupapi)
endif(WIN32)

add_executable(list_ports examples/list_ports.c)

target_link_libraries(list_ports libserialport)

