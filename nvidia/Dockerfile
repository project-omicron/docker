FROM projectomicron/omicron:base

# nvidia-docker does enable native support for Nvidia GPUs, however it doesn't ship support for OpenGL: https://github.com/NVIDIA/nvidia-docker/wiki#is-opengl-supported
# Thus you need to install OpenGL, see https://hub.docker.com/r/nvidia/opengl
# Commands used here are from https://github.com/machinekoder/nvidia-opengl-docker/blob/3a1bf3b9e75e0afaec16059c0c2c35ea1e65a328/README.md

RUN apt-get update && apt-get install -y --no-install-recommends \
        pkg-config \
        libxau-dev \
        libxdmcp-dev \
        libxcb1-dev \
        libxext-dev \
        libx11-dev && \
    rm -rf /var/lib/apt/lists/*

# replace with other Ubuntu version if desired
# see: https://hub.docker.com/r/nvidia/opengl/
# e.g. nvidia/opengl:1.1-glvnd-runtime-ubuntu16.04)
COPY --from=nvidia/opengl:1.0-glvnd-runtime-ubuntu18.04 \
  /usr/lib/x86_64-linux-gnu \
  /usr/lib/x86_64-linux-gnu

# replace with other Ubuntu version if desired
# see: https://hub.docker.com/r/nvidia/opengl/
# e.g. nvidia/opengl:1.1-glvnd-runtime-ubuntu16.04
COPY --from=nvidia/opengl:1.0-glvnd-runtime-ubuntu18.04 \
  /usr/share/glvnd/egl_vendor.d/10_nvidia.json \
  /usr/share/glvnd/egl_vendor.d/10_nvidia.json

RUN echo '/usr/lib/x86_64-linux-gnu' >> /etc/ld.so.conf.d/glvnd.conf && \
    ldconfig && \
    echo '/usr/$LIB/libGL.so.1' >> /etc/ld.so.preload && \
    echo '/usr/$LIB/libEGL.so.1' >> /etc/ld.so.preload

# nvidia-container-runtime
ENV NVIDIA_VISIBLE_DEVICES \
    ${NVIDIA_VISIBLE_DEVICES:-all}
ENV NVIDIA_DRIVER_CAPABILITIES \
    ${NVIDIA_DRIVER_CAPABILITIES:+$NVIDIA_DRIVER_CAPABILITIES,}graphics
