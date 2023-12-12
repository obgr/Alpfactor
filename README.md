# Codename AlpFactor

An Experimental alpine based image for the Recore A7 3d printer mainboard.

Current state: Unfinished, Not working, Not building.

## Why?

Less is more.

Is it viable to make a slimmer image?

## Requirements to run ARM images on x86

- Debian 12
- Docker version 24.0.7

```bash
$ sudo apt install qemu-system binfmt-support qemu-user-static
$ sudo docker run --rm --privileged multiarch/qemu-user-static --reset -p yes
$ sudo docker run -it  arm64v8/alpine:3.18 uname -m
# WARNING: The requested image's platform (linux/arm64/v8) does not match the detected host platform (linux/amd64/v4) and no specific platform was requested
# aarch64
```

success?

## Building  Dependencies

Before incorperating everything in the Dockerized build.
The dependencies should be translated into alpine packages.

Is it overengineered to split the dependenciy build flows into separate containers? (IMPORT alpine as dep1-builder)

### arm-trusted firmware

```bash
sudo apt install make gcc gcc-aarch64-linux-gnu
```

Compile

```bash
# git clone
# patch in changes
cd ~/git/arm-trusted-firmware
make CROSS_COMPILE=aarch64-linux-gnu- BL31=~/git/arm-trusted-firmware/build/sun50i_a64/debug/bl31.bin
```

### SPC Firmware

```bash
git clone https://github.com/crust-firmware/crust
cd crust
export CROSS_COMPILE=or1k-linux-musl-
make pine64_plus_defconfig
make scp
```

### u-boot

```bash
sudo apt install make gcc gcc-aarch64-linux-gnu bison flex ncurses-base swig libssl-dev
```

Compile

```bash
# git clone
# patch files

cd ~/git/u-boot

# Compile SPL/u-boot
$ make clean
$ export CROSS_COMPILE=aarch64-linux-gnu-
$ make pine64_plus_defconfig
$ make
# Compile arm
make CROSS_COMPILE=aarch64-linux-gnu- BL31=~/git/arm-trusted-firmware/build/sun50i_a64/debug/bl31.bin recore_defconfig

make CROSS_COMPILE=aarch64-linux-gnu- BL31=~/git/arm-trusted-firmware/build/sun50i_a64/debug/bl31.bin
```
