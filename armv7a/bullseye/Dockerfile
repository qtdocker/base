FROM multiarch/debian-debootstrap:armhf-bullseye

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update && apt full-upgrade -y && apt install -y --no-install-recommends \
    clang \
    ninja-build \
    git \
    locales \
    sudo \
    curl \
    build-essential \
    pkg-config \
    python3 \
    perl \
    ca-certificates \  
    file \
    wget \
    gnupg2 \
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/*    

RUN wget -q -O - https://files.pvs-studio.com/etc/pubkey.txt | apt-key add -

RUN wget -O /etc/apt/sources.list.d/viva64.list https://files.pvs-studio.com/etc/viva64.list    
    
RUN apt update  && apt install -y --no-install-recommends \
    libssl-dev \
    libffi-dev \
    pvs-studio \
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/*

ENV CC=/usr/bin/clang

ENV CXX=/usr/bin/clang++

WORKDIR /tmp

RUN git clone https://github.com/Kitware/CMake.git -b release

WORKDIR /tmp/CMake

RUN ./bootstrap
    
RUN make

RUN make install

WORKDIR /tmp

RUN rm -rf CMake

# Reconfigure locale
RUN locale-gen en_US.UTF-8 && dpkg-reconfigure locales

# Add group & user + sudo
RUN groupadd -r user && useradd --create-home --gid user user && echo 'user ALL=NOPASSWD: ALL' > /etc/sudoers.d/user

USER user
WORKDIR /home/user
ENV HOME /home/user

ENV CC=/usr/bin/clang

ENV CXX=/usr/bin/clang++

USER root

RUN apt update  && apt install -y --no-install-recommends \
    python3-pip \
    python3-setuptools \
    python3-dev \
    python3-wheel \
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/*

USER user

ENV PATH "$PATH:/home/user/.local/bin"

RUN pip3 install conan
