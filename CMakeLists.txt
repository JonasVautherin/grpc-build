cmake_minimum_required(VERSION 3.1)
project(third_party)

set(DEPS_BUILD_PATH "${PROJECT_BINARY_DIR}" CACHE PATH "Build path")
set(DEPS_INSTALL_PATH "${DEPS_BUILD_PATH}/install" CACHE PATH "Install path")

include(cmake/build_target.cmake)

list(APPEND CMAKE_PREFIX_PATH "${DEPS_INSTALL_PATH}")

build_target(zlib)
build_target(libressl)
build_target(cares)
build_target(protobuf)
build_target(grpc)
