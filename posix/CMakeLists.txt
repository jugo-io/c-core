

set(POSIX_SRC
    pubnub_version_posix.c
    pubnub_generate_uuid_posix.c
    pbpal_posix_blocking_io.c
    msstopwatch_monotonic_clock.c
    pbtimespec_elapsed_ms.c
    posix_socket_blocking_io.c
    pb_sleep_ms.c
)

add_library(pubnub_posix STATIC ${POSIX_SRC})
target_link_libraries(pubnub_posix PUBLIC pubnub_core)










# ../core/pbcc_set_state.c
# ../core/pubnub_pubsubapi.c
# ../core/pubnub_coreapi.c
# ../core/pubnub_coreapi_ex.c
# ../core/pubnub_ccore_pubsub.c
# ../core/pubnub_ccore.c
# ../core/pubnub_netcore.c
# ../lib/sockets/pbpal_sockets.c
# ../lib/sockets/pbpal_resolv_and_connect_sockets.c
# ../lib/sockets/pbpal_handle_socket_error.c
# ../core/pubnub_alloc_std.c
# ../core/pubnub_assert_std.c
# ../core/pubnub_generate_uuid.c
# ../core/pubnub_blocking_io.c
# ../core/pubnub_timers.c
# ../core/pubnub_json_parse.c
# ../lib/md5/md5.c
# ../lib/base64/pbbase64.c
# ../lib/pb_strnlen_s.c
# ../lib/pb_strncasecmp.c
# ../core/pubnub_helper.c
# ../core/pubnub_generate_uuid_v3_md5.c
# ../core/pubnub_free_with_timeout_std.c
# ../core/pubnub_url_encode.c
# ../core/pubnub_memory_block.c

