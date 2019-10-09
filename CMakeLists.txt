cmake_minimum_required(VERSION 3.1...3.14)

if(${CMAKE_VERSION} VERSION_LESS 3.12)
  cmake_policy(VERSION ${CMAKE_MAJOR_VERSION}.${CMAKE_MINOR_VERSION})
endif()

project(am LANGUAGES CXX)

set(HEADERS am.h halfint.h halfint_fmt.h
            racah_reduction.h rme.h
            wigner_gsl.h wigner_gsl_twice.h)
set(SOURCES am.cpp halfint.cpp)
set(TARGET am)

add_library(${TARGET} STATIC ${SOURCES} ${HEADERS})

target_link_libraries(${TARGET} PUBLIC m fmt::fmt)

target_link_libraries(${TARGET} PUBLIC Eigen3::Eigen)

find_package(GSL REQUIRED)
target_link_libraries(${TARGET} PUBLIC GSL::gsl GSL::gslcblas)

target_include_directories(${TARGET} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/..)
