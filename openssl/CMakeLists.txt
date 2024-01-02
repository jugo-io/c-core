set(CALLBACK_INTF_SOURCE
    pubnub_ntf_callback_posix.c
    pubnub_get_native_socket.c
)
set(WINDOWS_SRC
    pbpal_openssl.c
    pbpal_connect_openssl.c
    pbpal_add_system_certs_windows.c
    pbpal_openssl_blocking_io.c
    pbaes256.c
)

set(POSIX_SRC
    pbpal_openssl.c
    pbpal_connect_openssl.c
    pbpal_add_system_certs_posix.c
    pbpal_openssl_blocking_io.c
    pbaes256.c
)

if (UNIX)
    set(SRC ${CALLBACK_INTF_SOURCE} ${POSIX_SRC})
    set(LIBS)
elseif(WIN32)
    set(SRC ${CALLBACK_INTF_SOURCE} ${WINDOWS_SRC})
    set(LIBS)
else()
    message(FATAL_ERROR "Unsupported platform")
endif()

find_package(OpenSSL REQUIRED)

add_library(pubnub-openssl STATIC ${SRC})
target_link_libraries(pubnub-openssl OpenSSL::SSL OpenSSL::Crypto ${LIBS})
target_include_directories(pubnub-openssl PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/..)