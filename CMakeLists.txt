cmake_minimum_required(VERSION 3.22)
project(pubnub)

# Function to convert between "ON"/"OFF" and 1/0
function(num_option name description default)
    option(${name} ${description} ${default})
    if(${name})
        set(${name} 1 PARENT_SCOPE)
        message (STATUS "[*] ${name}")
    else()
        set(${name} 0 PARENT_SCOPE)
        message (STATUS "[ ] ${name}")
    endif()
endfunction()


message(STATUS "PubNub Options:")
num_option(ONLY_PUBSUB_API "Only pubsub API" OFF)
num_option(USE_PROXY "Use proxy" ON)
num_option(USE_GZIP_COMPRESSION "Use gzip compression" ON)
num_option(RECEIVE_GZIP_RESPONSE "Use gzip decompression" ON)
num_option(USE_SUBSCRIBE_V2 "Use subscribe v2" ON)
num_option(USE_ADVANCED_HISTORY "Use advanced history" ON)
num_option(USE_OBJECTS_API "Use objects API" ON)
num_option(USE_AUTO_HEARTBEAT "Use auto heartbeat" ON)
num_option(USE_ACTIONS_API "Use actions API" ON)
num_option(USE_REVOKE_TOKEN_API "Use revoke token API" OFF)
num_option(USE_GRANT_TOKEN_API "Use grant token API" OFF)
num_option(USE_FETCH_HISTORY "Use fetch history" ON)
num_option(USE_OPENSSL "Use OpenSSL" ON)

num_option(USE_CRYPTO_API "Use crypto API [OPENSSL ONLY]" OFF)
if (USE_CRYPTO_API AND NOT USE_OPENSSL)
    message(FATAL_ERROR "USE_OPENSSL requires USE_CRYPTO_API")
endif()


num_option(USE_STATIC_LIB "Use static library" OFF)
num_option(USE_CALLBACK_API "Use callback API [CALLBACK=ON SYNC=OFF]" OFF)

num_option(WITH_EXAMPLES "Build all examples" OFF)
num_option(WITH_TESTS "Build all tests" OFF)

add_subdirectory(posix)
add_subdirectory(core)
add_subdirectory(openssl)