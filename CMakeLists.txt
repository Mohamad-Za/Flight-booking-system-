cmake_minimum_required(VERSION 3.15)
project(FlightBookingSystem VERSION 1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Compiler warnings
if(MSVC)
    add_compile_options(/W4)
else()
    add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# Collect all source files
set(SOURCES
    main.cpp
    System.cpp
    Booking.cpp
    Flight.cpp
    Passenger.cpp
    Economy.cpp
    Business.cpp
)

add_executable(FlightBookingSystem ${SOURCES})

# Copy data files to build directory so the executable can find them
configure_file(${CMAKE_SOURCE_DIR}/flights.txt
               ${CMAKE_BINARY_DIR}/flights.txt COPYONLY)

if(EXISTS ${CMAKE_SOURCE_DIR}/bookings.txt)
    configure_file(${CMAKE_SOURCE_DIR}/bookings.txt
                   ${CMAKE_BINARY_DIR}/bookings.txt COPYONLY)
endif()
