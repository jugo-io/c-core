set(CORE_SRC
    pbcc_set_state.c
    pubnub_pubsubapi.c
    pubnub_coreapi.c
    pubnub_ccore_pubsub.c
    pubnub_ccore.c
    pubnub_netcore.c
    pubnub_alloc_static.c
    pubnub_assert_std.c
    pubnub_json_parse.c
    pubnub_helper.c
    pubnub_url_encode.c
    ../lib/pb_strnlen_s.c
    ../lib/pb_strncasecmp.c
    ../lib/base64/pbbase64.c
    pubnub_coreapi_ex.c
)

if (RECEIVE_GZIP_RESPONSE)
    list(APPEND CORE_SRC pbgzip_decompress.c)
endif()

if (USE_ADVANCED_HISTORY)
    list(APPEND CORE_SRC pbcc_advanced_history.c pubnub_advanced_history.c)
endif()

if (USE_FETCH_HISTORY)
    list(APPEND CORE_SRC pbcc_fetch_history.c pubnub_fetch_history.c)
endif()

add_library(pubnub_core STATIC ${CORE_SRC})
target_include_directories(pubnub_core PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/..
    ${CMAKE_CURRENT_SOURCE_DIR}/../openssl
    ${CMAKE_CURRENT_SOURCE_DIR}/../lib/base64)

target_compile_definitions(pubnub_core PUBLIC
    -DPUBNUB_THREADSAFE
    -DPUBNUB_LOG_LEVEL=PUBNUB_LOG_LEVEL_WARNING
    -DPUBNUB_ONLY_PUBSUB_API=${ONLY_PUBSUB_API}
    -DPUBNUB_PROXY_API=${USE_PROXY}
    -DPUBNUB_USE_GZIP_COMPRESSION=${USE_GZIP_COMPRESSION}
    -DPUBNUB_RECEIVE_GZIP_RESPONSE=${RECEIVE_GZIP_RESPONSE}
    -DPUBNUB_USE_SUBSCRIBE_V2=${USE_SUBSCRIBE_V2}
    -DPUBNUB_USE_OBJECTS_API=${USE_OBJECTS_API}
    -DPUBNUB_USE_ACTIONS_API=${USE_ACTIONS_API}
    -DPUBNUB_USE_ADVANCED_HISTORY=${USE_ADVANCED_HISTORY}
    -DPUBNUB_USE_AUTO_HEARTBEAT=${USE_AUTO_HEARTBEAT}
    -DPUBNUB_USE_GRANT_TOKEN_API=${USE_GRANT_TOKEN}
    -DPUBNUB_USE_REVOKE_TOKEN_API=${USE_REVOKE_TOKEN}
    -DPUBNUB_USE_FETCH_HISTORY=${USE_FETCH_HISTORY}
    -DPUBNUB_CALLBACK_API=${USE_CALLBACK_API})

set_target_properties(pubnub_core PROPERTIES LANGUAGE C)