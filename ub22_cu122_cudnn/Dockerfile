FROM nvidia/cuda:12.2.2-cudnn8-devel-ubuntu22.04
# CUDA11.2, cudnn8.1.1

# Maintainer Information
LABEL maintainer="wengkunduo@gmail.com"

RUN apt-get update

# 關閉互動模式
ENV DEBIAN_FRONTEND=noninteractive

## NVIDIA GraphicsCard parameter
ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES all

# 接收外部參數
ARG USER=initial
ARG UID=1000
ARG GROUP=initial
ARG GID=1000

# Switch apt source to Taiwan's mirror
RUN sed -i 's@archive.ubuntu.com@tw.archive.ubuntu.com@g' /etc/apt/sources.list

# Update and Install Packages
RUN apt-get update && apt-get install -y \
    software-properties-common \
    at-spi2-core \
    htop sudo git wget curl \
    byobu zsh \
    terminator \
    dbus-x11 libglvnd0 libgl1 libglx0 libegl1 libxext6 libx11-6 libxtst6 libinih-dev\
    nano vim \
    gnome-terminal libcanberra-gtk-module libcanberra-gtk3-module \
    python3-wheel python3-pip python3-dev python3-setuptools \
    libopencv-dev \
    openssh-server \
    cmake && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*



# 創建一個名為initial的用戶和用戶組
RUN groupadd -g $GID $GROUP && \
    useradd -m -u $UID -g $GID -s /bin/bash $USER && \
    echo "${USER} ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/${USER} && \
    chmod 0440 /etc/sudoers.d/${USER}




#=========================================================
#    Installing python packages 
#=========================================================
# ROBOTIS DYNAMIXEL
# RUN pip3 install pynput

# Timezone
RUN echo "tzdata tzdata/Areas select Asia" | debconf-set-selections && \
    echo "tzdata tzdata/Zones/Asia select Taipei" | debconf-set-selections && \
    apt-get update && apt-get install -y tzdata && \
    ln -snf /usr/share/zoneinfo/$TIME_ZONE /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir -p /home/${USER}/.config/terminator/

WORKDIR /home/${USER}
USER ${USER}

RUN mkdir work
WORKDIR /home/${USER}/work

CMD ["terminator"]
USER $USER


