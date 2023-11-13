file(GLOB_RECURSE sources
	"${CMAKE_CURRENT_SOURCE_DIR}/*.h"
	"${CMAKE_CURRENT_SOURCE_DIR}/*.hpp"
	"${CMAKE_CURRENT_SOURCE_DIR}/*.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/*.cpp")

if(MSVC_IDE)
	# Macro to preserve source files hierarchy in the IDE
	macro(GroupSources curdir)
		file(GLOB children RELATIVE ${PROJECT_SOURCE_DIR}/${curdir} ${PROJECT_SOURCE_DIR}/${curdir}/*)

		foreach(child ${children})
			if(IS_DIRECTORY ${PROJECT_SOURCE_DIR}/${curdir}/${child})
				GroupSources(${curdir}/${child})
			else()
				string(REPLACE "/" "\\" groupname ${curdir})
				string(REPLACE "src" "Sources" groupname ${groupname})
				source_group(${groupname} FILES ${PROJECT_SOURCE_DIR}/${curdir}/${child})
			endif()
		endforeach()
	endmacro()

	GroupSources(${CMAKE_CURRENT_SOURCE_DIR})
endif()

add_executable(shader-analyzer ${sources})

target_link_libraries(shader-analyzer PUBLIC
	SPIRV-Tools-opt
)
