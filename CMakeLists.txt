CMAKE_MINIMUM_REQUIRED(VERSION 3.8)

SET(INSTALL_PREFIX "/usr/local")

ADD_DEFINITIONS(-Wall -Wextra -Wno-unknown-pragmas)
ADD_DEFINITIONS(-fPIC) # for the static library which can be linked into the shared .so object.
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} g -Wno-sign-compare")
#ADD_COMPILE_OPTIONS ( -Wno-reorder )

option(CMAKE_INSTALL_DO_STRIP "install-strip" ON)

ADD_EXECUTABLE(tcpfwd ./src/ps_epoll.h ./src/tcpfwd.c)
target_compile_features(tcpfwd PRIVATE cxx_std_11)
ADD_EXECUTABLE(udpfwd ./src/ps_epoll.h ./src/udpfwd.c)
target_compile_features(udpfwd PRIVATE cxx_std_11)

########### Add all target ###############
ADD_CUSTOM_TARGET(generate_all)
ADD_DEPENDENCIES(generate_all tcpfwd udpfwd)

########### Add uninstall target ###############
CONFIGURE_FILE(
        "${CMAKE_CURRENT_SOURCE_DIR}/cmake_uninstall.cmake.in"
        "${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake"
        IMMEDIATE @ONLY)
ADD_CUSTOM_TARGET(remove_all "${CMAKE_COMMAND}" -P "${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake")

INSTALL(TARGETS tcpfwd DESTINATION ${INSTALL_PREFIX}/bin)
INSTALL(TARGETS udpfwd DESTINATION ${INSTALL_PREFIX}/bin)
