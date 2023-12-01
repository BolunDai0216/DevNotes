# Stage 1: CUDA-TensorRT base
FROM nvidia/cuda:12.1.1-cudnn8-devel-ubuntu20.04 AS cuda-tensorrt

ENV TRT_VERSION 8.6.1.6
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    cuda-toolkit-12-config-common \
    cuda-toolkit-config-common

RUN rm -rf /var/lib/apt/lists/*

# Stage 2: ROS base
FROM osrf/ros:noetic-desktop-full

ENV DEBIAN_FRONTEND=noninteractive
ENV CUDA_HOME /usr/local/cuda
ENV PATH $PATH:/usr/local/cuda/bin
ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:/usr/local/cuda/lib64:/usr/lib/x86_64-linux-gnu

COPY --from=cuda-tensorrt /usr/local/cuda /usr/local/cuda
COPY --from=cuda-tensorrt /usr/lib/x86_64-linux-gnu /usr/lib/x86_64-linux-gnu

RUN apt-get update && apt-get install -y \
    curl \
    gnupg2 \
    lsb-release \
    python3 \
    python3-pip \
    cmake \
    git \
    libboost-python-dev \
    software-properties-common

RUN python3 -m pip install mujoco

CMD ["bash"]