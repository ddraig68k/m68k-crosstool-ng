# Building the m68k-elf Toolchain with Crosstool-NG

This project uses **[Crosstool-NG](https://github.com/crosstool-ng/crosstool-ng)** to build a complete `m68k-elf` cross-compiler toolchain for the Y Ddraig 68k system.

This runs under Linux and will product either a Linux toolchain or a native Windows toolchain compiled using mingw.

This has curently been tested with _**Crosstools-NG 1.28**_ running under Debian, Ubuntu and WSL2/Ubuntu. 

This will build the toolchain with GCC 13 + Binutils 2.43 + GDB 13.2 along with the custom [Newlib](https://github.com/ddraig68k/newlib-cygwin) for Y Dddraig.

---

## Installing Crosstool-NG

Install the required build packages using your system package manager.

#### Debian / Ubuntu
```bash
sudo apt update
sudo apt install unzip wget git make autoconf automake build-essential libtool pkg-config gperf gawk bison flex texinfo help2man libncurses5-dev libncursesw5-dev python3 python3-yaml gettext libexpat1-dev libz-dev
```

### Install Crosstools-NG
```bash
git clone https://github.com/crosstool-ng/crosstool-ng.git
cd crosstool-ng
./bootstrap
./configure
make
sudo make install
```

```bash
sudo apt install mingw-w64 mingw-w64-tools binutils-mingw-w64-x86-64 gcc-mingw-w64-x86-64 g++-mingw-w64-x86-64 zlib1g-dev

```

### Building m68k-ddraig-elf for Linux

To build the compiler for Linux, run the following.

```bash
cp linux.config defconfig
ct-ng defconfig
ct-ng build
```

After a successful build, you’ll have a working toolchain under: `~x-tools/m68k-ddraig-elf`.
You can now add `~/x-tools/m68k-elf/bin` to your PATH.

### Building m68k-ddraig-elf for Windows

To build the compiler under Windows, Crosstool-NG uses the MinGW compiler to produce Window native binaries. You will need to install them if needed.

```bash
sudo apt install mingw-w64 mingw-w64-tools binutils-mingw-w64-x86-64 gcc-mingw-w64-x86-64 g++-mingw-w64-x86-64 zlib1g-dev
```

To build the compiler for Windows

```bash
cp windows.config defconfig
ct-ng defconfig
ct-ng build
```

After a successful build, you’ll have a working toolchain under: `~x-tools/HOST-x86_64-w64-mingw32/m68k-ddraig-elf`.
This can be copied to Windows and will run natively.


