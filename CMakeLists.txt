cmake_minimum_required(VERSION 3.15)

set(libsphinx5prealpha_VERSION 1.0.0)

projectlibsphinx5prealpha
	VERSION ${libsphinx5prealpha_VERSION}
	DESCRIPTION "Dependencies for using pocketsphinx in an app"
	HOMEPAGE_URL "https://github.com/smbika007/LibSphinx5prealpha"
	LANGUAGES CXX)

include(CMakePackageConfigHelpers)
include(GNUInstallDirs)

# add_library(beicode src/beicode.cpp include/beicode.h)
# add_library(beicode::beicode ALIAS beicode)

# if(BUILD_SHARED_LIBS AND WIN32)
	# target_compile_definitions(beicode
		# PRIVATE "BEICODE_EXPORT=__declspec(dllexport)"
		# INTERFACE "BEICODE_EXPORT=__declspec(dllimport)")
# endif()

# target_compile_features(beicode PUBLIC cxx_std_17)
target_include_directories(libsphinx5prealpha
	PUBLIC
		$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
		$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>)

configure_package_config_file(cmake/config.cmake.in
	${CMAKE_CURRENT_BINARY_DIR}/libsphinx5prealpha-config.cmake
	INSTALL_DESTINATION ${CMAKE_INSTALL_DATADIR}/libsphinx5prealpha
	NO_SET_AND_CHECK_MACRO)
write_basic_package_version_file(
	${CMAKE_CURRENT_BINARY_DIR}/libsphinx5prealpha-config-version.cmake
	VERSION ${libsphinx5prealpha}
	COMPATIBILITY SameMajorVersion)
install(
	FILES
		${CMAKE_CURRENT_BINARY_DIR}/libsphinx5prealpha-config.cmake
		${CMAKE_CURRENT_BINARY_DIR}/libsphinx5prealpha-config-version.cmake
	DESTINATION
		${CMAKE_INSTALL_DATADIR}/libsphinx5prealpha)

install(TARGETS libsphinx5prealpha EXPORT libsphinx5prealpha-targets)
install(DIRECTORY include/ DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
install(EXPORT libsphinx5prealpha-targets
	NAMESPACE libsphinx5prealpha::
	DESTINATION ${CMAKE_INSTALL_DATADIR}/libsphinx5prealpha)
