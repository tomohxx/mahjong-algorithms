cmake_minimum_required(VERSION 3.15)

project(shanten-algorithms LANGUAGES CXX)

include(CMakePackageConfigHelpers)
include(ExternalProject)
include(GNUInstallDirs)

if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
  set(CMAKE_INSTALL_PREFIX "${CMAKE_BINARY_DIR}/install" CACHE PATH "Install path" FORCE)
endif()

set(COMMON_CMAKE_ARGS
  -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}
  -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
)

ExternalProject_Add(shanten-number
  GIT_REPOSITORY https://github.com/tomohxx/shanten-number.git
  GIT_TAG master
  CMAKE_ARGS ${COMMON_CMAKE_ARGS}
  STEP_TARGETS build install
  BUILD_ALWAYS OFF
)

ExternalProject_Add(necessary-and-unnecessary-tiles
  GIT_REPOSITORY https://github.com/tomohxx/necessary-and-unnecessary-tiles.git
  GIT_TAG master
  CMAKE_ARGS ${COMMON_CMAKE_ARGS}
  STEP_TARGETS build install
  BUILD_ALWAYS OFF
)

ExternalProject_Add(waits-predictor
  GIT_REPOSITORY https://github.com/tomohxx/waits-predictor.git
  GIT_TAG main
  CMAKE_ARGS ${COMMON_CMAKE_ARGS}
  STEP_TARGETS build install
  BUILD_ALWAYS OFF
)

ExternalProject_Add(score-calculator
  GIT_REPOSITORY https://github.com/tomohxx/score-calculator.git
  GIT_TAG main
  CMAKE_ARGS ${COMMON_CMAKE_ARGS}
  STEP_TARGETS build install
  BUILD_ALWAYS OFF
)

configure_package_config_file(
  cmake/MahjongConfig.cmake.in
  ${CMAKE_CURRENT_BINARY_DIR}/MahjongConfig.cmake
  INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/mahjong
)

install(
  FILES ${CMAKE_CURRENT_BINARY_DIR}/MahjongConfig.cmake
  DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/mahjong
)
