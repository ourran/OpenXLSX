include(ExternalProject)

#=======================================================================================================================
# Download and build the PugiXML library
#=======================================================================================================================
ExternalProject_Add(pugi
        GIT_REPOSITORY https://github.com/zeux/pugixml.git
        GIT_TAG 8436f2a
        INSTALL_DIR ${OPENXLSX_DEPENDENCIES}
        UPDATE_COMMAND ""
        CMAKE_ARGS
            -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
            -DCMAKE_C_COMPILER=${CMAKE_C_COMPILER}
            -DCMAKE_CXX_COMPILER=${CMAKE_CXX_COMPILER}
            -DCMAKE_POSITION_INDEPENDENT_CODE=ON
            -DCMAKE_INSTALL_PREFIX:PATH=<INSTALL_DIR>
            -DCMAKE_PREFIX_PATH:PATH=<INSTALL_DIR>
            -Wno-dev)

#=======================================================================================================================
# Download and build the zlib library
#=======================================================================================================================
ExternalProject_Add(zlib
        GIT_REPOSITORY https://github.com/madler/zlib.git
        GIT_TAG cacf7f1
        INSTALL_DIR ${OPENXLSX_DEPENDENCIES}
        UPDATE_COMMAND ""
        CMAKE_ARGS
            -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
            -DCMAKE_C_COMPILER=${CMAKE_C_COMPILER}
            -DCMAKE_CXX_COMPILER=${CMAKE_CXX_COMPILER}
            -DCMAKE_POSITION_INDEPENDENT_CODE=ON
            -DCMAKE_INSTALL_PREFIX:PATH=<INSTALL_DIR>
            -DCMAKE_PREFIX_PATH:PATH=<INSTALL_DIR>
            -Wno-dev)

#=======================================================================================================================
# Download and build the libzip library
#=======================================================================================================================
ExternalProject_Add(libzip
        GIT_REPOSITORY https://github.com/nih-at/libzip.git
        GIT_TAG ff55682
        INSTALL_DIR ${OPENXLSX_DEPENDENCIES}
        UPDATE_COMMAND ""
        CMAKE_ARGS
            -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
            -DCMAKE_C_COMPILER=${CMAKE_C_COMPILER}
            -DCMAKE_CXX_COMPILER=${CMAKE_CXX_COMPILER}
            -DENABLE_COMMONCRYPTO=OFF
            -DENABLE_GNUTLS=OFF
            -DENABLE_MBEDTLS=OFF
            -DENABLE_OPENSSL=OFF
            -DENABLE_BZIP2=OFF
            -DBUILD_TOOLS=OFF
            -DBUILD_REGRESS=OFF
            -DBUILD_EXAMPLES=OFF
            -DBUILD_DOC=OFF
            -DENABLE_WINDOWS_CRYPTO=OFF
            -DCMAKE_POSITION_INDEPENDENT_CODE=ON
            -DBUILD_SHARED_LIBS=OFF
            -DCMAKE_INSTALL_PREFIX:PATH=<INSTALL_DIR>
            -DCMAKE_PREFIX_PATH:PATH=<INSTALL_DIR>
            -Wno-dev)

#=======================================================================================================================
# Load the OpenXLSX library folder
#=======================================================================================================================
include_directories(SYSTEM ${OPENXLSX_DEPENDENCIES}/include)
add_subdirectory(@openxlsx)

#=======================================================================================================================
# Define Dependencies
#=======================================================================================================================
ExternalProject_Add_StepDependencies(libzip install zlib)
add_dependencies(OpenXLSX pugi libzip)
