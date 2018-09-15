cmake_minimum_required(VERSION 3.1)
project(imgui)

set(IMGUI_DIR ${CMAKE_CURRENT_SOURCE_DIR})

set(IMGUI_SOURCES
	${IMGUI_DIR}/imconfig.h
	${IMGUI_DIR}/imgui.cpp
	${IMGUI_DIR}/imgui.h
	${IMGUI_DIR}/imgui_draw.cpp
	${IMGUI_DIR}/imgui_internal.h
	${IMGUI_DIR}/imgui_widgets.cpp
	${IMGUI_DIR}/imstb_rectpack.h
	${IMGUI_DIR}/imstb_textedit.h
	${IMGUI_DIR}/imstb_truetype.h
)

add_library(${PROJECT_NAME} STATIC ${IMGUI_SOURCES})

include_directories(${IMGUI_DIR})

if(APPLE)
	LIST(APPEND IMGUI_CFLAGS -fvisibility=hidden)
	if(IOS)
		LIST(APPEND IMGUI_CFLAGS -fembed-bitcode)
	endif(IOS)
	target_compile_options(${PROJECT_NAME} PUBLIC ${IMGUI_CFLAGS})
endif()

set_target_properties (${PROJECT_NAME} PROPERTIES DEBUG_POSTFIX "d")

INSTALL(TARGETS ${PROJECT_NAME}
	RUNTIME DESTINATION bin
	LIBRARY DESTINATION lib
	ARCHIVE DESTINATION lib
)

INSTALL(FILES
	${IMGUI_DIR}/imconfig.h
	${IMGUI_DIR}/imgui.h
	${IMGUI_DIR}/imgui_internal.h
	${IMGUI_DIR}/imstb_rectpack.h
	${IMGUI_DIR}/imstd_textedit.h
	${IMGUI_DIR}/imstd_truetype.h
	DESTINATION include/imgui
)
