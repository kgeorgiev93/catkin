cmake_minimum_required(VERSION 2.8.3)

set(catkin_EXTRAS_DIR ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

include(cmake/HunterGate.cmake)
HunterGate(
    URL "https://github.com/ruslo/hunter/archive/v0.20.36.tar.gz"
    SHA1 "9cbf5d9c7ee37c61d903b7f8751dc79d67eb26b4"
)

project(catkin)

if(NOT DEFINED CATKIN_TOPLEVEL)
  include(${catkin_EXTRAS_DIR}/all.cmake NO_POLICY_SCOPE)
endif()

catkin_package()

install(FILES LICENSE
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

# install cmake files for catkin (except some files only used at build time of catkin)
install(DIRECTORY cmake
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
  USE_SOURCE_PERMISSIONS
  PATTERN "catkinConfig.cmake.in" EXCLUDE)

catkin_python_setup()

if(CATKIN_ENABLE_TESTING)
  catkin_add_nosetests(test/local_tests)
  catkin_add_nosetests(test/unit_tests)
endif()
