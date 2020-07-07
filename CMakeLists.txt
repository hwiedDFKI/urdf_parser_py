cmake_minimum_required(VERSION 2.8 FATAL_ERROR)
project(urdfdom_py)

# find_package(catkin REQUIRED)
# catkin_package()
#
# catkin_python_setup()
#
# catkin_install_python(PROGRAMS
#   scripts/display_urdf
#   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )
#
# if (CATKIN_ENABLE_TESTING)
#   catkin_add_nosetests(test/test_urdf.py)
#   catkin_add_nosetests(test/test_urdf_error.py)
# endif()

if(PYTHON_EXECUTABLE)
    message(STATUS "Defined python executable is: ${PYTHON_EXECUTABLE}")
    set(Python_EXECUTABLE ${PYTHON_EXECUTABLE})
elseif("$ENV{PYTHON}" STREQUAL "")
    # https://cmake.org/cmake/help/v3.12/module/FindPython.html
    find_package(Python COMPONENTS Interpreter)
else()
    set(PYTHON $ENV{PYTHON})
    message(STATUS ${PYTHON})
endif()


message(STATUS "Using python: ${Python_EXECUTABLE}")
message(STATUS "Detected python version: ${Python_VERSION}")


install(
    CODE "execute_process(
    COMMAND ${Python_EXECUTABLE} -m pip install -U ${CMAKE_SOURCE_DIR}
    WORKING_DIRECTORY ${CMAKE_SOURCE_DIR})"
)
