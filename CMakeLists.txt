cmake_minimum_required(VERSION 3.5)

project(gicp LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(GICP_HEADERS    gicp.h
                    optimize.h
                    # bfgs_funcs.h
                    transform.h
                    scan.h
                    nanoflann.hpp
                    )

set(GICP_SOURCES    gicp.cpp
                    optimize.cpp
                    bfgs_funcs.cpp
                    transform.cpp
                    scan.cpp
                    )

add_library(gicp            ${GICP_SOURCES}
                            ${GICP_HEADERS}
                            )

add_executable(test_gicp    test_gicp.cpp
                            ${GICP_SOURCES}
                            ${GICP_HEADERS}
                            )

target_link_libraries(gicp      gsl
                                gslcblas
                                )

target_link_libraries(test_gicp gsl
                                gslcblas
                                boost_program_options
                                boost_system
                                )

set(S2A_HEADERS     scan.h
                    # scan2ascii.h
                    transform.h
                    )

set(S2A_SOURCES     scan.cpp
                    scan2ascii.cpp
                    transform.cpp
                    )

add_executable(scan2ascii   ${S2A_SOURCES}
                            ${S2A_HEADERS}
                            )

target_link_libraries(scan2ascii    boost_program_options
                                    boost_system
                                    )
