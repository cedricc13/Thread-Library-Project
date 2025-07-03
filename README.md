# Thread Library Project - Operating Systems Course

## Copyright Notice
© 2025 Maulard Jules - François Mathieu - Larragueta César - Derache Cédric. All rights reserved.

This project was developed as part of an Operating Systems course by a team of students who contributed equally to all aspects of the development. The project was originally developed on a private institutional Git repository (Thor forge) and has been migrated to this public repository, which explains the single commit history. No part of this project may be reproduced, distributed, or transmitted in any form or by any means without the prior written permission of the authors.

## Description
This project implements a user-space thread library with cooperative scheduling (no preemption) using a FIFO policy. The library provides an interface similar to `pthread.h` for creating, managing, and synchronizing threads entirely in user space.

## Key Features
- **Cooperative Thread Scheduling**: FIFO-based non-preemptive scheduling
- **Thread Management**: Create, destroy, yield, join operations
- **Main Thread Integration**: The main function is treated as a thread
- **Performance Benchmarking**: Comparison tools with pthread implementation
- **Advanced Features Implemented**:
  - **Preemption**: Timer-based preemptive scheduling using alarms
  - **Priority Scheduling**: Thread priority management with starvation prevention
  - **Mutex Support**: Mutual exclusion primitives for thread synchronization

## Project Structure
```
├── src/                    # Source code for thread library
├── tests/                  # Test programs and benchmarks
├── install/               # Installation directory
│   ├── lib/              # Compiled library files
│   └── bin/              # Executable test programs
├── graphs/               # Performance comparison graphs
└── Makefile              # Build system
```

## Implementation Details

### Core Thread Operations
- `thread_create()`: Create new threads with specified functions
- `thread_yield()`: Voluntarily yield CPU to other threads
- `thread_join()`: Wait for thread termination
- `thread_self()`: Get current thread identifier
- `thread_exit()`: Terminate current thread

### Advanced Features
- **Preemption**: Implemented using SIGALRM for time-sliced scheduling
- **Priority Scheduling**: Threads can be assigned different priorities
- **Mutex Operations**: `thread_mutex_lock()`, `thread_mutex_unlock()` for synchronization

## Prerequisites
- GCC compiler
- Make
- Valgrind (for memory leak detection)
- gnuplot or Python/Matplotlib (for performance graphs)

## Installation and Usage

### Building the Project
```bash
# Default build - compile library and tests
make

# Build pthread versions for comparison
make pthreads

# Install compiled files
make install
```

### Running Tests
```bash
# Run all tests with reasonable parameters
make check

# Run tests under Valgrind
make valgrind

# Generate performance comparison graphs
make graphs
```

### Available Test Programs
The project includes comprehensive test programs:
- `01-main`: Basic thread creation and execution
- `02-switch`: Thread switching mechanisms
- `11-join`: Thread joining operations
- `21-create-many`: Mass thread creation tests
- `22-create-many-recursive`: Recursive thread creation
- `31-switch-many`: Context switching performance
- `32-switch-many-join`: Combined switching and joining
- `51-fibonacci`: Fibonacci calculation with threads
- `61-mutex`: Mutex synchronization tests
- `62-mutex-stress`: Stress testing for mutex operations
- `71-preemption`: Preemption functionality tests

### Performance Testing
The library includes custom performance tests:
- **Array Sum**: Parallel computation using divide-and-conquer
- **Parallel Sorting**: Multi-threaded sorting algorithms
- **Stress Tests**: High-load scenarios with many concurrent threads

## Architecture

### Scheduling Algorithm
- **Base Implementation**: Cooperative FIFO scheduling
- **Enhanced Version**: Preemptive scheduling with configurable time slices
- **Priority Support**: Multiple priority levels with round-robin within each level

### Memory Management
- Dynamic stack allocation for each thread
- Proper cleanup and leak prevention
- Valgrind integration for memory debugging

### Synchronization
- Mutex implementation using atomic operations
- Deadlock detection and prevention mechanisms
- Integration with preemptive scheduling

## Performance Comparison
The library includes comprehensive benchmarking against pthread:
- Thread creation overhead
- Context switching performance
- Scalability with increasing thread counts
- Memory usage patterns

Performance measurements are conducted on multi-core systems with proper CPU binding to ensure fair comparison.

## Build System
The Makefile provides the following targets:
- `make`: Default build
- `make check`: Run test suite
- `make valgrind`: Memory leak detection
- `make pthreads`: Build pthread versions
- `make graphs`: Generate performance graphs
- `make install`: Install to `install/` directory

## Testing and Validation
- **Correctness**: All test programs execute correctly
- **Memory Safety**: No memory leaks detected by Valgrind
- **Performance**: Benchmarking against pthread implementation
- **Robustness**: Stress testing with high thread counts

## Implementation Notes
- The library maintains O(1) complexity for core operations where possible
- Thread-safe operations using appropriate synchronization primitives
- Efficient data structures to minimize overhead
- Proper handling of edge cases and error conditions

## Academic Context
This project was developed as part of an Operating Systems course focusing on:
- Thread scheduling algorithms
- User-space thread implementation
- Performance analysis and optimization
- Memory management in multi-threaded environments
- Synchronization primitives and their implementation

## Technical Specifications
- **Language**: C (following pthread.h interface conventions)
- **Scheduling**: Cooperative FIFO with preemptive extensions
- **Synchronization**: Mutex support with advanced features
- **Platform**: POSIX-compliant systems
- **Performance**: Optimized for multi-core architectures
