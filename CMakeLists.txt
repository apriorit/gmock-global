cmake_minimum_required(VERSION 3.6)

project(gmock-global LANGUAGES CXX)

# check if building as a stand-alone project
if(CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME)
    set(IS_TOPLEVEL_PROJECT TRUE)
else()
    set(IS_TOPLEVEL_PROJECT FALSE)
endif()

# options
option(GMOCK_GLOBAL_BUILD_SAMPLES "Build ${PROJECT_NAME} samples" ${IS_TOPLEVEL_PROJECT})

# make sure install paths work on all platforms
include(GNUInstallDirs)

add_library(${PROJECT_NAME} INTERFACE)
add_library(${PROJECT_NAME}::${PROJECT_NAME} ALIAS ${PROJECT_NAME})

target_include_directories(${PROJECT_NAME}
    INTERFACE
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
)

if(GMOCK_GLOBAL_BUILD_SAMPLES)
    # add a pseudo-project to make plog headers visible in IDE
    file(GLOB_RECURSE ${PROJECT_NAME}_HEADERS ${CMAKE_CURRENT_SOURCE_DIR}/include/*.h)
    add_custom_target(${PROJECT_NAME}-headers SOURCES ${${PROJECT_NAME}_HEADERS})
    set_target_properties(${PROJECT_NAME}-headers PROPERTIES FOLDER Include)

    # add samples
    add_subdirectory(sample)
endif()