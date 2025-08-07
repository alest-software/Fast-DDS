cmake_minimum_required(VERSION 3.15)
project(fastdds_wrapper VERSION 3.3.0)

set(CMAKE_PREFIX_PATH "/opt/fastdds")
set(CMAKE_INSTALL_PREFIX "/opt/fastdds")
set(CPACK_PACKAGING_INSTALL_PREFIX "${CMAKE_INSTALL_PREFIX}")

set(save_cmake_project_name, "${CMAKE_PROJECT_NAME}")
set(CMAKE_PROJECT_NAME "fastdds")
add_subdirectory(Fast-DDS)
set(CMAKE_PROJECT_NAME, "${save_cmake_project_name}")

include(InstallRequiredSystemLibraries)

#message(STATUS "fastdds_VERSION = '${fastdds_VERSION}'")

if(NOT DEFINED CPACK_PACKAGE_VERSION)
    set(CPACK_PACKAGE_VERSION ${PROJECT_VERSION})
endif()

if(DEFINED CPACK_DEBIAN_PACKAGE_REVISION)
    set(CPACK_PACKAGE_VERSION "${CPACK_PACKAGE_VERSION}-${CPACK_DEBIAN_PACKAGE_REVISION}")
endif()

set(CPACK_PACKAGE_NAME "libfastdds")
set(CPACK_PACKAGE_CONTACT "you@example.com")
set(CPACK_DEBIAN_PACKAGE_DEPENDS "libc6")
set(CPACK_GENERATOR "DEB")

set(CPACK_PACKAGE_FILE_NAME "${CPACK_PACKAGE_NAME}_${CPACK_PACKAGE_VERSION}_${CPACK_DEBIAN_PACKAGE_ARCHITECTURE}")

include(CPack)

