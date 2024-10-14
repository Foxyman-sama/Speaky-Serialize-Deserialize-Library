cmake_minimum_required(VERSION 3.30)
project(proto_files)

find_package(Protobuf REQUIRED CONFIG)

add_library(${PROJECT_NAME} 
    new_connection.pb.cc
    message.pb.cc
)
target_include_directories(${PROJECT_NAME} PUBLIC 
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${Protobuf_INCLUDE_DIRS}
)
target_link_libraries(${PROJECT_NAME} PUBLIC 
   protobuf::libprotoc protobuf::libprotobuf 
)

protobuf_generate(TARGET ${PROJECT_NAME} PROTOS new_connection.proto)
protobuf_generate(TARGET ${PROJECT_NAME} PROTOS message.proto)