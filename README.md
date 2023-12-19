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

## Docker build

Its faster to Cross compile on x86, therefore we will do so where possible (for now).

```bash
cd ~/git/alpfactor
docker build -f docker/Dockerfile -t alpfactor:test .
```
