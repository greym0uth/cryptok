## Building

### Prerequisites

1. Make sure you have the following dependencies installed:

   * `g++` 5.1 or later or `clang++` 3.5 or later
   * `python` 3 or 2.7
   * GNU `make` 3.81 or later
   * `cmake` 3.4.3 or later
   * `ninja`
   * `curl`
   * `git`
   * `ssl` which comes in `libssl-dev` or `openssl-devel`
   * `pkg-config` if you are compiling on Linux and targeting Linux

2. Clone the repo with submodules:

``` sh
git clone --recurse-submodules https://github.com/Jaden-Giordano/cryptok
```

### Installing toolchain

You'll need to grab the latest xtensa-esp32s2-elf toolchain from [here](https://github.com/espressif/crosstool-NG/releases).

*Note:* Be sure to grab the the `esp32s2` one as well as right one for your machine (operating system); it will most likely be: `xtensa-esp32s2-elf-gcc8_4_0-esp-<version>-<os>-amd64.tar.gz`.

``` sh
mkdir ./esp
tar -xzf xtensa-esp32s2-elf-gcc8_4_0-esp-<version>-<os>-amd64.tar.gz -C ./esp
```

#### Building and Flashing tools

``` sh
cargo install cargo-espflash
# For python alternative (not recommended) use:
# pip install esptool 
```

### Configuring

rust-xtensa requires some setup which can be done by running the configure script and `setenv`:

``` sh
./configure
```

Before you build youll need to add the xtensa compilers to your path:

``` sh
source setenv
```

### Building & Flashing

To build:

``` sh
cd cryptok
cargo build
```

To flash:

``` sh
cd cryptok
cargo espflash --chip esp32 --example esp32 --speed 460800 /dev/ttyUSB0
```

