cmake_minimum_required(VERSION 2.8)

project(libmaxminddb C)

set(C_STANDARD 99)

include(TestBigEndian)
test_big_endian(BIG_ENDIAN)

if (BIG_ENDIAN)
  add_definitions(-DMMDB_LITTLE_ENDIAN=0)
else()
  add_definitions(-DMMDB_LITTLE_ENDIAN=1)
endif()

include_directories(include)
add_library(maxminddb STATIC src/maxminddb.c src/data-pool.c)
set_target_properties(maxminddb PROPERTIES PUBLIC_HEADER "include/maxminddb.h")

install(TARGETS maxminddb
  ARCHIVE DESTINATION lib
  PUBLIC_HEADER DESTINATION include)
