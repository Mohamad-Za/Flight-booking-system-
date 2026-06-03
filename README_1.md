# Flight Booking System

A console-based flight booking system written in C++, demonstrating object-oriented design, polymorphic passenger types, file persistence, and clean class separation.

## Overview

The system manages flights, passengers, and bookings through a menu-driven interface. Passenger data and bookings are persisted to disk across sessions.

```
┌─────────────┐       ┌───────────┐       ┌──────────────────┐
│   System    │ 1───* │  Booking  │ 1───1 │ Passenger (base) │
│ (orchestr.) │       │           │       │ ┌──────────────┐ │
│             │ 1───* │  Flight   │       │ │   Economy    │ │
└─────────────┘       └───────────┘       │ │   Business   │ │
                                          │ └──────────────┘ │
                                          └──────────────────┘
```

**Key design patterns used:**
- Polymorphism via abstract `Passenger` base class with `Economy` and `Business` subtypes
- Composition: `Booking` holds a `unique_ptr<Passenger>` and a `Flight`
- Single-responsibility: `System` acts as the service/orchestration layer
- File persistence: bookings serialised to `bookings.txt` on shutdown and restored on startup

## Features

- List all available flights
- Book a flight (Economy or Business class)
- View, search, and delete bookings
- Search passengers by name or SSN
- Data persisted to file between sessions

## Build

### Requirements

- C++17 compiler (GCC 9+, Clang 10+, MSVC 2019+)
- CMake 3.15+

### Steps

```bash
git clone https://github.com/Mohamad-Za/Flight-booking-system-c-.git
cd Flight-booking-system-c-
cmake -S . -B build
cmake --build build
./build/FlightBookingSystem
```

> **Note:** `flights.txt` must be present in the working directory when running the executable. A sample file is included in the repo root.

### Windows (Visual Studio)

Open the folder in Visual Studio 2019+ and use the built-in CMake support, or run the cmake commands above from a Developer Command Prompt.

## Project Structure

```
.
├── main.cpp              # Entry point and menu loop
├── System.h / .cpp       # Core orchestration layer
├── Booking.h / .cpp      # Booking entity
├── Flight.h / .cpp       # Flight entity
├── Passenger.h / .cpp    # Abstract passenger base
├── Economy.h / .cpp      # Economy subclass (baggage)
├── Business.h / .cpp     # Business subclass (meal preference)
├── flights.txt           # Seed data - available flights
├── bookings.txt          # Persisted booking records
└── CMakeLists.txt        # Cross-platform build config
```

## Data File Format

`flights.txt` - one flight per line, format: `<flight_number> <destination>`

```
SK101 Stockholm
LH202 Frankfurt
BA303 London
```

`bookings.txt` - serialised by `System::writeAllBookingsToFile()`. Regenerated on each run.

## License

MIT
