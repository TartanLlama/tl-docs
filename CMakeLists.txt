cmake_minimum_required(VERSION 3.8)

set(CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/cmake" ${CMAKE_MODULE_PATH})

find_package(Sphinx REQUIRED)

set(SPHINX_SOURCE ${CMAKE_CURRENT_SOURCE_DIR})
set(SPHINX_BUILD ${CMAKE_CURRENT_BINARY_DIR})
set(SPHINX_INDEX_FILE ${SPHINX_BUILD}/index.html)

add_custom_command(OUTPUT ${SPHINX_INDEX_FILE}
	COMMAND 
		${SPHINX_EXECUTABLE} -b html
		${SPHINX_SOURCE} ${SPHINX_BUILD}
  	WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
	DEPENDS 
		index.rst
		api/misc/apply.rst
		api/misc/casts.rst
		api/misc/decay_copy.rst
		api/misc/dependent_false.rst
		api/expected.rst
		api/function_ref.rst
		api/misc/index.rst
		api/misc/integer_sequence.rst
		api/misc/make_array.rst
		api/misc/numeric_aliases.rst
		api/optional.rst
		api/misc/overload.rst
		api/misc/type_traits.rst
		api/misc/typelist.rst
	MAIN_DEPENDENCY ${SPHINX_SOURCE}/conf.py
	COMMENT "Generating documentation with Sphinx")

 add_custom_target(Sphinx ALL DEPENDS ${SPHINX_INDEX_FILE})

 include(GNUInstallDirs)
 install(DIRECTORY ${SPHINX_BUILD}
	 DESTINATION ${CMAKE_INSTALL_DOCDIR})
