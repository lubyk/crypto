# --------------------------------------------------------------
#  crypto
#  
#  provides:
#    crypto.so
# --------------------------------------------------------------
set(MODULE_NAME crypto)
set(target ${MODULE_NAME})

find_package(OpenSSL REQUIRED)
include_directories(vendor/src ${OPENSSL_INCLUDE_DIR})

set(MODULE_SOURCES vendor/src/lcrypto.c)
add_library(${target} MODULE ${MODULE_SOURCES})
set_target_properties(${target}
  PROPERTIES
  LINK_FLAGS ${PLAT_OBJ_FLAGS}
  PREFIX ""
  SUFFIX ".so"
)  
target_link_libraries(${target} ${OPENSSL_LIBRARIES})

# --------------------------------------------------------------
#  install                                     
# --------------------------------------------------------------
install(TARGETS ${target}
  DESTINATION lib/lubyk
)
