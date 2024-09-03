# Sortledton Setup

## Pre-requisites
Make sure the following are installed on your system:
- O.S. Linux
- Autotools, Autoconf 2.69+
- A C++17 compliant compiler with support for OpenMP. The original code is tested with GCC 10. If there is a version difference, there could be some minor errors.
- libnuma 2.0 + (sudo apt-get install libnuma-dev)
- libpapi 5.5 +
- SQLite 3.27 + (sudo apt-get install sqlite3 libsqlite3-dev)
- Intel Threading Building Blocks 2 (version 2020.1-2)
- Disable NUMA balancing feature to avoid the Linux Kernel to swap pages during insertions: echo 0 | sudo tee  /proc/sys/kernel/numa_balancing


## Sortledton Installation
To install Sortledton, follow the steps below:

```bash
git clone https://gitlab.db.in.tum.de/per.fuchs/sortledton.git
cd sortledton
mkdir build && cd build
cmake -DCMAKE_BUILD_TYPE=Release ..
make sortledton
```

## Driver Installation
To install the driver, follow the steps below:

```bash
git clone https://github.com/PerFuchs/gfe_driver
cd gfe_driver
git submodule update --init
mkdir build && cd build
autoreconf -iv ..
```


## Configuration
To configure Sortledton, follow the steps below in the build directory of the gfe_driver:

```bash
../configure --enable-optimize --disable-debug --with-sortledton=/path/to/microbenchmark/build   
make -j
```

## Installing TBB
You will have to install Thread Building Blocks onto your local machine.

```bash
git clone https://github.com/oneapi-src/oneTBB.git
cd oneTBB
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX=/tmp/my_installed_onetbb -DTBB_TEST=OFF ..
cmake --build .
cmake --install .
```

Note that you need root access to your machine in order to install oneTBB, since it copies the files to  ```/lib/blabla```
