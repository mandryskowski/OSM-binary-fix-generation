# Generate protobuf sources
add_library(osmpbf STATIC)
protobuf_generate(
    TARGET osmpbf
    LANGUAGE cpp
    PROTOS fileformat.proto osmformat.proto
)
set_target_properties(osmpbf PROPERTIES
POSITION_INDEPENDENT_CODE ON
)

# Add static library
target_compile_features(osmpbf PUBLIC cxx_std_11)
target_link_libraries(osmpbf PRIVATE protobuf::libprotobuf)
target_include_directories(osmpbf SYSTEM PUBLIC ${Protobuf_INCLUDE_DIRS})

# Add shared library
#add_library(osmpbf_shared SHARED $<TARGET_OBJECTS:osmpbf>)
#target_compile_features(osmpbf_shared PUBLIC cxx_std_11)
#target_link_libraries(osmpbf_shared PRIVATE protobuf::libprotobuf)
#target_include_directories(osmpbf_shared SYSTEM PUBLIC ${Protobuf_INCLUDE_DIRS})
#set_target_properties(osmpbf_shared PROPERTIES OUTPUT_NAME osmpbf
#                                               VERSION ${PROJECT_VERSION}
#                                               SOVERSION ${PROJECT_VERSION_MAJOR})

# install(TARGETS osmpbf ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR})
# install(TARGETS osmpbf_shared LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})
# install(FILES ${CMAKE_SOURCE_DIR}/include/osmpbf/osmpbf.h
#               ${CMAKE_BINARY_DIR}/osmpbf/osmformat.pb.h
#               ${CMAKE_BINARY_DIR}/osmpbf/fileformat.pb.h
#         DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/osmpbf)
# 