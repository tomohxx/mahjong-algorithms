cmake_minimum_required(VERSION 3.15)

project(shanten-algorithms LANGUAGES CXX)

include(ExternalProject)

if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
  set(CMAKE_INSTALL_PREFIX "${CMAKE_BINARY_DIR}/install" CACHE PATH "Install path" FORCE)
endif()

set(COMMON_CMAKE_ARGS
  -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}
  -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
)

ExternalProject_Add(shanten-number
  GIT_REPOSITORY https://github.com/tomohxx/shanten-number.git
  GIT_TAG v2.0.1
  CMAKE_ARGS ${COMMON_CMAKE_ARGS}
  STEP_TARGETS build install
  BUILD_ALWAYS OFF
)

ExternalProject_Add(necessary-and-unnecessary-tiles
  GIT_REPOSITORY https://github.com/tomohxx/necessary-and-unnecessary-tiles.git
  GIT_TAG v2.0.1
  CMAKE_ARGS ${COMMON_CMAKE_ARGS}
  STEP_TARGETS build install
  BUILD_ALWAYS OFF
)

ExternalProject_Add(waits-predictor
  GIT_REPOSITORY https://github.com/tomohxx/waits-predictor.git
  GIT_TAG v1.0.1
  CMAKE_ARGS ${COMMON_CMAKE_ARGS}
  STEP_TARGETS build install
  BUILD_ALWAYS OFF
)

ExternalProject_Add(score-calculator
  GIT_REPOSITORY https://github.com/tomohxx/score-calculator.git
  GIT_TAG v0.2.0
  CMAKE_ARGS ${COMMON_CMAKE_ARGS}
  STEP_TARGETS build install
  BUILD_ALWAYS OFF
)

add_custom_target(build-all DEPENDS
  shanten-number-build
  necessary-and-unnecessary-tiles-build
  waits-predictor-build
  score-calculator-build
)

add_custom_target(install-all DEPENDS
  shanten-number-install
  necessary-and-unnecessary-tiles-install
  waits-predictor-install
  score-calculator-install
)
