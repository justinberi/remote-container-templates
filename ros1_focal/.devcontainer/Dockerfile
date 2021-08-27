# based on https://hub.docker.com/_/ros
FROM ubuntu:20.04 AS base

ARG USERNAME=ros
ARG USER_UID=1000
ARG USER_GID=$USER_UID
ARG ROS_DISTRO=noetic

ENV DEBIAN_FRONTEND=noninteractive

# Create a non-root user
# https://dev.to/emmanuelnk/using-sudo-without-password-prompt-as-non-root-docker-user-52bg
RUN apt-get update && apt-get install -y sudo \
&& adduser --disabled-password --gecos '' ${USERNAME} \
&& adduser ${USERNAME} sudo \
&& echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Install timezone
RUN ln -fs /usr/share/zoneinfo/UTC /etc/localtime \
  && export DEBIAN_FRONTEND=noninteractive \
  && apt-get update && apt-get install -y \
  tzdata \
  && dpkg-reconfigure --frontend noninteractive tzdata \
  && apt-get autoremove -y  && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Set local
RUN apt-get update && apt-get install \
  locales \
  && locale-gen en_US.UTF-8 \
  && update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 \
  && apt-get autoremove  && apt-get clean && rm -rf /var/lib/apt/lists/*
ENV LANG en_US.UTF-8

# Setup sources
RUN apt-get update && sudo apt-get install -y curl gnupg2 lsb-release \
    && echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list \
    && curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add

# Install the base
RUN apt-get update && apt-get install -y \
    ros-${ROS_DISTRO}-ros-base \
    python3-argcomplete

# Install the developer version
RUN apt-get update && apt-get install -y \
    ros-${ROS_DISTRO}-desktop
    
# Source the ros distro
RUN echo source /opt/ros/${ROS_DISTRO}/setup.bash >> /home/${USERNAME}/.bashrc

# nvidia-container-runtime
# As documented in http://wiki.ros.org/docker/Tutorials/Hardware%20Acceleration
ENV NVIDIA_VISIBLE_DEVICES \
    ${NVIDIA_VISIBLE_DEVICES:-all}
ENV NVIDIA_DRIVER_CAPABILITIES \
    ${NVIDIA_DRIVER_CAPABILITIES:+$NVIDIA_DRIVER_CAPABILITIES,}all

ENV DEBIAN_FRONTEND=