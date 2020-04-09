Docker setup
============

To make our setup reproducible, we use Docker.

Installation
------------

We use [x11docker](https://github.com/mviereck/x11docker) which is a wrapper around Docker that provides handy functionality such as easily enabling X applications and automatically creating the host's user and group in the container.

If you have a Nvidia graphics card, install `nvidia-container-toolkit` according to this guide: https://github.com/NVIDIA/nvidia-docker/wiki/Installation-(Native-GPU-Support)

Building
--------

Pre-built images are available at https://hub.docker.com/r/projectomicron/omicron.
You can build the images yourself like this:

    docker build -t projectomicron/omicron -t projectomicron/omicron:base base/
    docker build -t projectomicron/omicron:nvidia nvidia/

Usage
-----

You can enter the container like this:

    x11docker --quiet -i --hostdisplay --clipboard --gpu --sudouser --home=$PWD/home -- --shm-size=2G -- projectomicron/omicron bash

However, if you use a Nvidia graphics card, use this:

    x11docker --quiet -i --hostdisplay --clipboard --sudouser --home=$PWD/home -- --gpus all --shm-size=2G -- projectomicron/omicron:nvidia bash

In the command the following is happening:

* it enables you to open graphical programs,
* it uses the UID and GID of your current user so file permissions will not be screwed up,
* it mounts the directory `home` *in the current path* into the container's home directory, thus saving all changes to your home directory even after exiting the container.

Finally you can follow the commands from https://github.com/project-omicron/gazebo_simulation#how-to-use inside the container.

Note: The `sudo` password is `x11docker`.
