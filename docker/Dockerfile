# Not working because `nvidia/cuda:10.1-cudnn7-devel` cannot be found
# FROM nvidia/cuda:10.1-cudnn7-devel

FROM nvidia/cuda:11.2.2-cudnn8-devel-ubuntu20.04

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -y \
    python3-opencv \
    ca-certificates \
    python3-dev \
    python3-pip \
    git \
    wget \
    sudo \
    ninja-build \
    vim
RUN ln -sv /usr/bin/python3 /usr/bin/python

# create a non-root user
ARG USER_ID=1000
RUN useradd -m --no-log-init --system  --uid ${USER_ID} appuser -g sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
USER appuser
WORKDIR /home/appuser
ENV PATH="/home/appuser/.local/bin:${PATH}"

# install dependencies
# See https://pytorch.org/ for other options if you use a different version of CUDA
RUN pip install --user tensorboard cmake   # cmake from apt-get is too old
# RUN pip install --user torch==1.6.0+cu101 torchvision==0.7.0+cu101 -f https://download.pytorch.org/whl/cu101/torch_stable.html

# These versions are compatible with cuda 11.2.2.
# Please refer to https://github.com/pytorch/pytorch/issues/50032
RUN pip install --user torch==1.12.1+cu113 torchvision==0.13.1+cu113 -f https://download.pytorch.org/whl/cu113/torch_stable.html

# RUN pip install --user -i https://pypi.tuna.tsinghua.edu.cn/simple tensorboard opencv-python cython yacs termcolor scikit-learn tabulate gdown gpustat faiss-gpu ipdb h5py
COPY docker/requirements.txt .
RUN pip install -r requirements.txt
