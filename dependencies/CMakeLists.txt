# Enable fetching content
include(FetchContent)

# Set the root of the Terrapane source repositories
if(DEFINED ENV{TERRAPANE_SOURCE_URI})
    set(TERRAPANE_SOURCE_URI "$ENV{TERRAPANE_SOURCE_URI}")
else()
    set(TERRAPANE_SOURCE_URI "https://github.com/terrapane")
endif()

if(libkdf_BUILD_TESTS)
    # Fetch the Simple Test Framework library
    FetchContent_Declare(stf
        GIT_REPOSITORY ${TERRAPANE_SOURCE_URI}/stf.git
        GIT_TAG        v1.0.0
        GIT_SHALLOW    true)

    # It is not necessary to install the STF library
    set(stf_INSTALL OFF)

    # Make STF available
    FetchContent_MakeAvailable(stf)
endif()

# Fetch the Hashing library
FetchContent_Declare(libhash
    GIT_REPOSITORY ${TERRAPANE_SOURCE_URI}/libhash.git
    GIT_TAG        v1.0.0
    GIT_SHALLOW    true)

# Fetch the Security Utilities library
FetchContent_Declare(secutil
    GIT_REPOSITORY ${TERRAPANE_SOURCE_URI}/secutil.git
    GIT_TAG        v1.0.0
    GIT_SHALLOW    true)

# If not installing libkdf, turn off installation for dependencies
if(NOT libkdf_INSTALL)
    set(libhash_INSTALL OFF)
    set(secutil_INSTALL OFF)
endif()

# Make dependencies available
FetchContent_MakeAvailable(libhash secutil)
