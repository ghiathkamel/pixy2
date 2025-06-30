# Running Pixy2 Software on Raspberry Pi 4

This repository primarily targets the Pixy2 hardware which uses an LPC43xx
microcontroller. The code under `src/device` depends heavily on that hardware.
Running those firmware sources directly on a Raspberry Pi would require a
complete rewrite of the low level drivers (camera, I/O, USB, servo control,
image capture, etc.) and is therefore outside the scope of this repository.

However, the host-side tools and libraries build and run on Linux, including the
Raspberry Pi. These programs communicate with a Pixy2 camera connected over USB
or other supported interfaces. To compile them natively on a Raspberry Pi 4
running Raspberry Pi OS, use the steps below.

## Install build dependencies

```bash
sudo apt-get update
sudo apt-get install g++ make libusb-1.0-0-dev qtbase5-dev python3-dev
```

## Clone the repository

```bash
git clone https://github.com/charmedlabs/pixy2.git
cd pixy2/scripts
```

## Build the host tools

Running `build_all.sh` will compile the PixyMon GUI, the C++ examples, the
Python bindings and the USB library. The binaries will be placed in the `build`
directory.

```bash
./build_all.sh
```

After compilation you can run PixyMon from `build/pixymon/PixyMon` or use the
examples located in the corresponding `build` subfolders.

## Notes on firmware porting

The firmware found under `src/device` is tightly coupled to the LPC43xx
microcontroller used on Pixy2. Porting it to run directly on a Raspberry Pi
would require replacing the hardware abstraction layers with code that uses the
Pi's camera interface and peripherals. This is a significant engineering effort
and is not currently provided in the upstream project.
