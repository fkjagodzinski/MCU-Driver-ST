# MCU-Driver-HAL Tests

This directory contains the build instructions for the tests defined in the _MCU-Driver-HAL_ repository.

Each test build instructions provides access to hardware specific source code and link with the example main algorithm provided as a library that is linked to the executable.

## Building the test

Each test can be built by doing the following:

1. Clone the repository **recursively** to fetch both `MCU-Driver-HAL` and `MCU-Driver-HAL/tools/greentea-client`:

    ```
    git clone --recursive git@github.com:ARMmbed/MCU-Driver-ST.git
    ```

1. Change the current working directory to `MCU-Driver-ST/sdfx_st/tests/mbed_hal/<TEST>/`.
1. Generate the build system files:

    ```
    cmake -S ./ -B cmake_build/ -DGREENTEA_CLIENT_STDIO=OFF -DMBED_TOOLCHAIN=<TOOLCHAIN> -DCMAKE_BUILD_TYPE=debug
    ```

    If you prefer to use the Ninja build system rather than the UNIX Makefiles, append `-G Ninja` to the command above.
1. Build:

    ```
    cmake --build cmake_build/
    ```

Outcome: The test compiles, links and produces artefacts.

## Running the test

1. Change the current working directory to `MCU-Driver-ST/`.

1. Use `mbedhtrun` to flash and run the test:

    ```
    mbedhtrun -f ./sdfx_st/tests/mbed_hal/<TEST>/cmake_build/<TEST_BINARY_NAME>.bin -e MCU-Driver-HAL/tests/host_tests/ -d <TARGET_PLATFORM_MOUNT_POINT> -p <TARGET_PLATFORM_SERIAL_PORT>
    ```

    You can append multiple `-v` flags to `mbedhtrun` command to increase verbosity, i.e. `-vv`.
