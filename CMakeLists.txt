cmake_minimum_required(VERSION 3.1)
project(bundle)

#file(GLOB_RECURSE source_files  )
#file(GLOB_RECURSE header_files  )

add_library(bundle 
	${PROJECT_SOURCE_DIR}/bundle.cpp
	${PROJECT_SOURCE_DIR}/bundle.hpp
)

target_include_directories(bundle PUBLIC ${PROJECT_SOURCE_DIR}/ )

if(MSVC)
    target_compile_definitions(bundle PUBLIC 
		-D_CRT_SECURE_NO_WARNINGS
		-D_SCL_SECURE_NO_WARNINGS
	)
endif()

#------------------------------------------------

add_executable( bundle_tests ${PROJECT_SOURCE_DIR}/tests.cxx )
target_include_directories(bundle_tests PUBLIC ${PROJECT_SOURCE_DIR}/ )
target_link_libraries( bundle_tests bundle )

#------------------------------------------------

add_executable( bundle_bench ${PROJECT_SOURCE_DIR}/bench.cxx )
target_include_directories(bundle_bench PUBLIC ${PROJECT_SOURCE_DIR}/ )
target_link_libraries( bundle_bench bundle )