# Note: list of traces is created at cmake time, not build time
file(GLOB test_trace_files
	"${CMAKE_CURRENT_SOURCE_DIR}/../../../test/trace_files/*.scap")

foreach(trace_file_path ${test_trace_files})
	get_filename_component(trace_file ${trace_file_path} NAME)
	add_custom_target(docker-local-trace-${trace_file} ALL
		DEPENDS ${CMAKE_CURRENT_BINARY_DIR}/${trace_file})
	add_custom_command(OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/${trace_file}
		COMMAND ${CMAKE_COMMAND} -E copy ${trace_file_path} ${CMAKE_CURRENT_BINARY_DIR}/${trace_file}
		DEPENDS ${trace_file_path})
endforeach()

