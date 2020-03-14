cmake_minimum_required(VERSION 3.11)

include(${CMAKE_CURRENT_SOURCE_DIR}/../../script/max-pretarget.cmake)

add_library(
	${PROJECT_NAME}
	MODULE
  bufGranul2~_DSP.c
  bufGranul2~.c  
)

include(${CMAKE_CURRENT_SOURCE_DIR}/../../script/max-posttarget.cmake)
