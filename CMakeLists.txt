cmake_minimum_required(VERSION 3.11)
################################################################################
# Paths
set(MAX_SDK_PATH "" CACHE PATH "Path to the Max SDK")
if(NOT MAX_SDK_PATH)
  message(FATAL_ERROR "Max SDK Path is not set")
endif()

if (APPLE)
	set(CMAKE_OSX_ARCHITECTURES x86_64-d)
  set(CMAKE_XCODE_GENERATE_SCHEME ON)
  set(CMAKE_XCODE_SCHEME_EXECUTABLE "/Applications/Max.app")
  set(CMAKE_OSX_DEPLOYMENT_TARGET 10.12 CACHE STRING "")
endif()

################################################################################
# Main Action
project (gmu_objects LANGUAGES C)

set(CMAKE_XCODE_GENERATE_TOP_LEVEL_PROJECT_ONLY ON)
set(AUTHOR_DOMAIN "org.gmem.gmu")
string(TIMESTAMP "%Y" THISYEAR)
set_property(GLOBAL PROPERTY USE_FOLDERS ON)
################################################################################
# Misc setup and subroutines
include("${CMAKE_CURRENT_SOURCE_DIR}/src/script/max-package.cmake")

################################################################################
# Generate a project for every folder in the "source/projects" folder
SUBDIRLIST(PROJECT_DIRS "${CMAKE_CURRENT_SOURCE_DIR}/src/projects")
foreach (project_dir ${PROJECT_DIRS})
	if (EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/src/projects/${project_dir}/CMakeLists.txt")
		message("Generating: ${MAX_TARGET_NAMESPACE}${project_dir}")
		add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/src/projects/${project_dir}")
	endif ()
endforeach ()
