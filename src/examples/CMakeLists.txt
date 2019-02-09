IF (!MSVC)
	ADD_COMPILE_OPTIONS(-Wno-unused-result)
endif()

SET(TARGETS
    lasexample
    lasexample_write_only
    lasexample_add_rgb
    lasexample_simple_classification
    lasexample_write_only_with_extra_bytes)

FOREACH(TARGET ${TARGETS})
  ADD_EXECUTABLE(${TARGET} ${TARGET}.cpp)
  TARGET_LINK_LIBRARIES(${TARGET} LASlib)
#   set_target_properties(${TARGET} PROPERTIES
#       RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR})
ENDFOREACH(TARGET)
