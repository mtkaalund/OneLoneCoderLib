cmake_minimum_required( VERSION 3.10 )
project(olcPixelGameEngine VERSION 2.0.3 LANGUAGES CXX)

find_package(Threads REQUIRED)
find_package(X11 REQUIRED)
find_package(OpenGL REQUIRED)
find_package(PNG REQUIRED)

add_library(${PROJECT_NAME} src/olcPixelGameEngine.cc)

target_compile_features(${PROJECT_NAME} INTERFACE cxx_std_17)

target_include_directories(${PROJECT_NAME}
    PUBLIC
     ${CMAKE_CURRENT_SOURCE_DIR}/include/
    $<BUILD_INTERFACE:${${PROJECT_NAME}}/include>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
    )

target_link_libraries(${PROJECT_NAME}
	${CMAKE_THREAD_LIBS_INIT}
	${X11_X11_LIB}
	${OPENGL_gl_LIBRARY}
	${PNG_LIBRARIES}
	-lstdc++fs
    )

if(USE_OLC_GRAPHICS2D)
	add_library(olcPGEX_Graphics2D src/Extensions/olcPGEX_Graphics2D.cc)
	target_compile_features(olcPGEX_Graphics2D INTERFACE cxx_std_17)

	target_include_directories(olcPGEX_Graphics2D
	    PUBLIC
	     ${CMAKE_CURRENT_SOURCE_DIR}/include/
	    $<BUILD_INTERFACE:${${PROJECT_NAME}}/include>
	    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
 	   )

	target_link_libraries(olcPGEX_Graphics2D
		${CMAKE_THREAD_LIBS_INIT}
		${X11_X11_LIB}
		${OPENGL_gl_LIBRARY}
		${PNG_LIBRARIES}
		-lstdc++fs
    	olcPixelGameEngine
    	)
endif()

if(USE_OLC_GRAPHICS3D)
	add_library(olcPGEX_Graphics3D src/Extensions/olcPGEX_Graphics3D.cc)
	target_compile_features(olcPGEX_Graphics3D INTERFACE cxx_std_17)

	target_include_directories(olcPGEX_Graphics3D
	    PUBLIC
	     ${CMAKE_CURRENT_SOURCE_DIR}/include/
	    $<BUILD_INTERFACE:${${PROJECT_NAME}}/include>
	    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
	    )

	target_link_libraries(olcPGEX_Graphics3D
		${CMAKE_THREAD_LIBS_INIT}
		${X11_X11_LIB}
		${OPENGL_gl_LIBRARY}
		${PNG_LIBRARIES}
		-lstdc++fs
	    olcPixelGameEngine
	
	    )
endif()

if(USE_OLC_SOUND)
	add_library(olcPGEX_Sound src/Extensions/olcPGEX_Sound.cc)
	target_compile_features(olcPGEX_Sound INTERFACE cxx_std_17)

	target_include_directories(olcPGEX_Sound
	    PUBLIC
	     ${CMAKE_CURRENT_SOURCE_DIR}/include/
	    $<BUILD_INTERFACE:${${PROJECT_NAME}}/include>
	    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
	    )

	target_link_libraries(olcPGEX_Sound
		${CMAKE_THREAD_LIBS_INIT}
		${X11_X11_LIB}
		${OPENGL_gl_LIBRARY}
		${PNG_LIBRARIES}
		-lstdc++fs
		-lasound
	    olcPixelGameEngine
	    )
endif()

if(USE_OLC_POPUP)
	add_library(olcPGEX_PopUpMenu src/Extensions/olcPGEX_PopUpMenu.cc)
	target_compile_features(olcPGEX_PopUpMenu INTERFACE cxx_std_17)
	target_include_directories(olcPGEX_PopUpMenu
		PUBLIC
		${CMAKE_CURRENT_SOURCE_DIR}/include/
		$<BUILD_INTERFACE:${${PROJECT_NAME}}/include>
		$<INSTALL_INTERFACE:${CMAKE_INSTAL_INCLUDEDIR}>
		)
	target_link_libraries(olcPGEX_PopUpMenu
		${CMAKE_THREAD_LIBS_INIT}
		${X11_X11_LIB}
		${OPENGL_gl_LIBRARY}
		${PNG_LIBRARIES}
		-stdc++fs
		olcPixelGameEngine
		)
endif()
