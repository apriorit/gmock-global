####################################################
# Reference values for GMOCK_GLOBAL_GTEST_GIT_TAG:
#
# release-1.8.1
# release-1.10.0
# release-1.11.0
# release-1.12.0
# release-1.12.1
# v1.13.0
# v1.14.0
# v1.15.0
# v1.15.1
# v1.15.2
#
####################################################

if(NOT DEFINED GMOCK_GLOBAL_GTEST_GIT_TAG)
  set(GMOCK_GLOBAL_GTEST_GIT_TAG "release-1.11.0")
endif()

include(FetchContent)

FetchContent_Declare(
  googletest
  GIT_REPOSITORY "https://github.com/google/googletest.git"
  GIT_TAG ${GMOCK_GLOBAL_GTEST_GIT_TAG}
)

# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

FetchContent_MakeAvailable(googletest)

if(CMAKE_COMPILER_IS_GNUCXX)
    target_compile_options(gtest PUBLIC -Wno-maybe-uninitialized)
endif()

add_executable(sample main.cpp)
target_link_libraries(sample gmock-global::gmock-global gmock_main)