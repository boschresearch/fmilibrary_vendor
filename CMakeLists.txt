cmake_minimum_required(VERSION 2.8.3)
project(fmilibrary_vendor)

include(ExternalProject)
externalproject_add(FMILibraryProject
  URL https://jmodelica.org/fmil/FMILibrary-2.0.3-src.zip
  URL_MD5 53d8edd7442c31bcd3fb56477e574845
  TIMEOUT 60
)
externalproject_get_property(FMILibraryProject INSTALL_DIR)
set(FMILibraryProject_INCLUDE_DIR "${INSTALL_DIR}/src/install/include")
set(FMILibraryProject_LIB_DIR "${INSTALL_DIR}/src/install/lib")

find_package(catkin)
catkin_package(
  INCLUDE_DIRS include
  LIBRARIES fmilib_shared
)
add_library(fmilib_shared SHARED IMPORTED)
set_target_properties(fmilib_shared PROPERTIES IMPORTED_LOCATION ${FMILibraryProject_LIB_DIR}/libfmilib_shared.so)
add_dependencies(fmilib_shared FMILibraryProject)

install(FILES ${FMILibraryProject_LIB_DIR}/libfmilib_shared.so
  DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
)

install(DIRECTORY ${FMILibraryProject_INCLUDE_DIR}
  DESTINATION .
)

