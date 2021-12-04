# Attempt to convert _vmmouse.c_ into Rust

This repository consists of our (Nitheesh P, Sairam G and Shriram R) attempt to convert 
the Linux kernel driver _vmmouse.c_ into Rust. 

# Build Instructions

- Step 1: Setup the Ubuntu Xenial Xerus 16.04.7
version of Linux in your Virtual Box environment
which has the Linux Kernel version v4.15 running
on it. The link to this OS distribution can be found
at [Ubuntu Xerial](https://releases.ubuntu.com/16.04/ubuntu-16.04.7-desktop-amd64.iso).

- Step 2: Install rust using the following command:
```
$ curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
Then run the following to install the nightly build toolchains for Rust.
```
rustup toolchain install nightly
```
After this, the following command is to be run in order to set the nightly release of the compiler to
default.
```
rustup default nightly
```

- Step 3: Run the following command in the root directory:
```
cargo build
```

- Step 4: Run the following commands in the vmmouse directory:
```
RUST_TARGET_PATH=\$(pwd)/.. cargo xbuild --target x86_64-linux-kernel-module
```
Then run
```
make
```
This makes the source files and generates the psmouse.ko module which can be inserted with the
following command:
```
sudo insmod psmouse.ko
```
The output that the module is loaded and the Rust function is called by the C file (psmouse-base.c)
can be seen by viewing the dmesg output.
```
dmesg | tail
```
