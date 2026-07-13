cmake_minimum_required(VERSION 3.16)
project(PacketAnalyzer VERSION 1.0)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Header files location

include_directories(${CMAKE_SOURCE_DIR}/include)

find_package(Threads REQUIRED)

# Packet parser viewer executable
add_executable(packet_analyzer
    src/main.cpp
    src/pcap_reader.cpp
    src/packet_parser.cpp
)

# Simple DPI executable
add_executable(dpi_simple
    src/main_working.cpp
    src/pcap_reader.cpp
    src/packet_parser.cpp
    src/sni_extractor.cpp
    src/types.cpp
)

# Multi-threaded DPI executable
add_executable(dpi_engine
    src/dpi_mt.cpp
    src/pcap_reader.cpp
    src/packet_parser.cpp
    src/sni_extractor.cpp
    src/types.cpp
)
target_link_libraries(dpi_engine PRIVATE Threads::Threads)

# For macOS, we might need to link against system libraries later

if(APPLE)
    # Add any macOS-specific settings here
endif()
