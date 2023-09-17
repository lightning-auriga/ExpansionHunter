cmake_minimum_required(VERSION 3.13)
project(ExpansionHunter)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Check for required packages:
find_package(ZLIB REQUIRED)
find_package(BZip2 REQUIRED)
find_package(LibLZMA REQUIRED)
find_package(CURL REQUIRED)

include(ExternalProject)
set(installDir ${CMAKE_CURRENT_BINARY_DIR}/install)


ExternalProject_Add(ehunter
	SOURCE_DIR ${CMAKE_SOURCE_DIR}/ehunter
	BUILD_ALWAYS YES
	TEST_COMMAND "ctest"
	CMAKE_ARGS -DCMAKE_INSTALL_PREFIX:PATH=${installDir}
		-DCMAKE_PREFIX_PATH:PATH=${installDir}
		-DCMAKE_C_COMPILER=${CMAKE_C_COMPILER}
		-DCMAKE_CXX_COMPILER=${CMAKE_CXX_COMPILER}
		-DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE} ${CMAKE_SOURCE_DIR}/ehunter
)


ExternalProject_Add_StepDependencies(ehunter configure)
