cmake_minimum_required(VERSION 3.1)

project(external-grpc)
include(ExternalProject)

list(APPEND CMAKE_ARGS
    "-DCMAKE_INSTALL_PREFIX:PATH=${CMAKE_INSTALL_PREFIX}"
    "-DCMAKE_PREFIX_PATH=${CMAKE_PREFIX_PATH}"
    "-DCMAKE_TOOLCHAIN_FILE:PATH=${CMAKE_TOOLCHAIN_FILE}"
    "-DZLIB_ROOT=${CMAKE_INSTALL_PREFIX}"
    "-DOPENSSL_ROOT_DIR=${CMAKE_INSTALL_PREFIX}"
    "-DRUN_HAVE_STD_REGEX=0"
    "-DRUN_HAVE_POSIX_REGEX=0"
    "-DRUN_HAVE_STEADY_CLOCK=0"
    "-DgRPC_BUILD_TESTS=OFF"
    "-DgRPC_ZLIB_PROVIDER=package"
    "-DgRPC_CARES_PROVIDER=package"
    "-DgRPC_PROTOBUF_PROVIDER=package"
    "-DgRPC_PROTOBUF_PACKAGE_TYPE=CONFIG"
    "-DgRPC_SSL_PROVIDER=package"
    "-DgRPC_INSTALL_default=ON"
    "-DgRPC_MSVC_STATIC_RUNTIME=OFF"
    "-DgRPC_BUILD_CSHARP_EXT=OFF"
    )

if(IOS)
    list(APPEND CMAKE_ARGS
        "-DPLATFORM=${PLATFORM}"
        "-DgRPC_BUILD_CODEGEN=OFF"
        )
endif()

message(STATUS "Preparing external project \"grpc\" with args:")
foreach(CMAKE_ARG ${CMAKE_ARGS})
    message(STATUS "-- ${CMAKE_ARG}")
endforeach()

ExternalProject_add(
    grpc
    URL https://github.com/grpc/grpc/archive/v1.21.0.zip
    PREFIX grpc
    CMAKE_ARGS "${CMAKE_ARGS}"
    )
