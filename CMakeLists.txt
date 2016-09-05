CMAKE_MINIMUM_REQUIRED(VERSION 3.5)

set(CMAKE_USER_MAKE_RULES_OVERRIDE
   ${CMAKE_CURRENT_SOURCE_DIR}/c_flag_overrides.cmake)
set(CMAKE_USER_MAKE_RULES_OVERRIDE_CXX
   ${CMAKE_CURRENT_SOURCE_DIR}/cxx_flag_overrides.cmake)

PROJECT(CMakeCPPTemplate)

IF(MSVC)
# make sure that we use the Unicode version of the Win API functions
ADD_DEFINITIONS( -DUNICODE -D_UNICODE )
ENDIF()

INCLUDE_DIRECTORIES(
"${PROJECT_SOURCE_DIR}/src"
"${PROJECT_SOURCE_DIR}/src/include"
"${PROJECT_SOURCE_DIR}/include"
)

IF( CMAKE_SIZEOF_VOID_P EQUAL 8 )
  # if win32
  link_directories(
  "${PROJECT_SOURCE_DIR}/lib/win64"
  )
ELSE( CMAKE_SIZEOF_VOID_P EQUAL 8 )
  # else win64
  link_directories(
  "${PROJECT_SOURCE_DIR}/lib/win32"
  )
ENDIF( CMAKE_SIZEOF_VOID_P EQUAL 8 )

# add Source Code
FILE (
GLOB_RECURSE
SRC_FILES
${PROJECT_SOURCE_DIR}/src/*.hpp
${PROJECT_SOURCE_DIR}/include/*.hpp
${PROJECT_SOURCE_DIR}/src/*.cpp
)

# set build target
# executable ( Windows program )
# ADD_EXECUTABLE( CMakeCPPTemplate WIN32 "${SRC_FILES}" )
# executable ( console )
ADD_EXECUTABLE( CMakeCPPTemplate "${SRC_FILES}" )
# library static
# ADD_LIBRARY ( CMakeCPPTemplate STATIC)
# library shared
# ADD_LIBRARY ( CMakeCPPTemplate SHARED)

# ==== unittests ====
#ADD_SUBDIRECTORY ( ${PROJECT_SOURCE_DIR}/third_party/googletest-1.7.0 )
#FILE (
#GLOB_RECURSE
#TEST_FILES
#${PROJECT_SOURCE_DIR}/test/*.hpp
#${PROJECT_SOURCE_DIR}/test/*.cpp
#${PROJECT_SOURCE_DIR}/include/*.hpp
#)

#SET( GTEST_ROOT ${PROJECT_SOURCE_DIR}/third_party/googletest-1.7.0 )
#INCLUDE_DIRECTORIES( ${GTEST_ROOT}/include )

#ENABLE_TESTING()
#ADD_EXECUTABLE ( unit_test ${TEST_FILES} ${GTEST_ROOT}/src/gtest_main.cc )
#TARGET_LINK_LIBRARIES( unit_test gtest gtest_main )

#ADD_TEST( NAME unit_test COMMAND unit_test )
