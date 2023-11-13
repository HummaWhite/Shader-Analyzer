cmake_minimum_required(VERSION 3.0)

project(Shader_Analyzer)

add_subdirectory(spirv-tools)
add_subdirectory(src)

target_include_directories(shader-analyzer
	PRIVATE
	"${CMAKE_CURRENT_SOURCE_DIR}/external/spirv-headers/include"
	"${CMAKE_CURRENT_SOURCE_DIR}/spirv-tools/include"
)

set_property(TARGET shader-analyzer PROPERTY FOLDER "Shader-Analyzer")
