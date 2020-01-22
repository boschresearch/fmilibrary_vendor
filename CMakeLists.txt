cmake_minimum_required(VERSION 3.5)
project(fmilibrary_vendor)

find_package(ament_cmake REQUIRED)

include(ExternalProject)
externalproject_add(FMILibraryProject
  GIT_REPOSITORY https://github.com/modelon-community/fmi-library.git
  GIT_TAG 2.1
  TIMEOUT 60
)
externalproject_get_property(FMILibraryProject INSTALL_DIR)
set(FMILibraryProject_INCLUDE_DIR "${INSTALL_DIR}/src/install/include")
set(FMILibraryProject_LIB_DIR "${INSTALL_DIR}/src/install/lib")

install(DIRECTORY ${FMILibraryProject_INCLUDE_DIR}/ DESTINATION include)
install(FILES ${FMILibraryProject_LIB_DIR}/libfmilib.a DESTINATION lib)
install(FILES ${FMILibraryProject_LIB_DIR}/libfmilib_shared.so DESTINATION lib)

ament_export_include_directories(include)
ament_export_libraries(libfmilib.a libfmilib_shared.so)
ament_package()
