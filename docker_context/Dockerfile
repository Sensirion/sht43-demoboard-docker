FROM ubuntu:22.04

ENV LANG C.UTF-8

# Work around apt-get hanging during install because it tries to query the user
ARG DEBIAN_FRONTEND=noninteractive

# Upgrade system and install base packages
RUN apt-get update --fix-missing\
  && apt-get -qy upgrade \
  && apt-get -qy install --no-install-recommends \
    build-essential \
    cmake  \
    clang-format \
    clang-tidy \
    cppcheck \
    graphviz \
    # Ninja
    ninja-build \
    libncurses5 \
    libc++abi-dev \
    libc++-dev \
    # plant uml
	  plantuml \
    # python pip
	  python3-pip \
    unzip \
    tree \
    wget \
  && apt-get -qy clean \
  && rm -rf /var/lib/apt/lists/*

ARG GCC_ARM_VERSION=10.3-2021.10
# Install GNU ARM GCC (the version from apt-get is older)
RUN wget "https://developer.arm.com/-/media/Files/downloads/gnu-rm/$GCC_ARM_VERSION/gcc-arm-none-eabi-$GCC_ARM_VERSION-x86_64-linux.tar.bz2" --no-check-certificate \
  && tar -xf "gcc-arm-none-eabi-$GCC_ARM_VERSION-x86_64-linux.tar.bz2" -C /opt \
  && rm "gcc-arm-none-eabi-$GCC_ARM_VERSION-x86_64-linux.tar.bz2"
ENV PATH="${PATH}:/opt/gcc-arm-none-eabi-$GCC_ARM_VERSION:/opt/gcc-arm-none-eabi-$GCC_ARM_VERSION/bin"

# Install specific version of Doxygen (apt-get provides an older, buggy version)
ARG DOXYGEN_VERSION=1.9.7
RUN wget "https://www.doxygen.nl/files/doxygen-$DOXYGEN_VERSION.linux.bin.tar.gz" --no-check-certificate \
&& tar -xf "doxygen-$DOXYGEN_VERSION.linux.bin.tar.gz" -C /opt \
&& rm "doxygen-$DOXYGEN_VERSION.linux.bin.tar.gz"
ENV PATH="${PATH}:/opt/doxygen-$DOXYGEN_VERSION/bin"

#install required python packages
RUN pip3 install editorconfig-checker==2.0.3 \
  && pip3 install codespell==2.2.4
