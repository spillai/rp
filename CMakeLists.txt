SET(PROJECT_NAME RP)
PROJECT(${PROJECT_NAME})
cmake_minimum_required(VERSION 2.4.6)
CMAKE_POLICY(VERSION 2.8)

IF (COMMAND cmake_policy)
  CMAKE_POLICY(SET CMP0003 NEW)
ENDIF (COMMAND cmake_policy)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS}  -Wall  -O3 -march=native ")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall  -O3 -march=native")

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
# LIST(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake_modules)

find_package(OpenCV REQUIRED)
# find_package(Eigen3 REQUIRED)
# find_package(Cholmod REQUIRED)
# FIND_PACKAGE(Boost REQUIRED COMPONENTS thread system)


include_directories(
    ${PROJECT_SOURCE_DIR}/src
)

add_library(${PROJECT_NAME} SHARED
    src/stopwatch/Stopwatch.cpp
    src/stopwatch/Stdafx.cpp
)

target_link_libraries(${PROJECT_NAME}
    ${OpenCV_LIBS}
)

file(GLOB RP_HDRS ${PROJECT_SOURCE_DIR}/src/*.h ${PROJECT_SOURCE_DIR}/src/*.hpp)
install(FILES ${RP_HDRS} DESTINATION ${CMAKE_INSTALL_PREFIX}/include/rp/)
INSTALL(TARGETS ${PROJECT_NAME} DESTINATION ${CMAKE_INSTALL_PREFIX}/lib )

# INSTALL(DIRECTORY ${PROJECT_SOURCE_DIR}/include DESTINATION ${CMAKE_INSTALL_PREFIX}/include/rp)

