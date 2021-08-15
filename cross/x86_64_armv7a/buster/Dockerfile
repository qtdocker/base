FROM atom63/qt-docker:linux-buster-x86_64

USER root

RUN dpkg --add-architecture armhf && apt update 

RUN apt install -y build-essential \
    pkg-config \
    binutils:amd64 \
    gcc-8-arm-linux-gnueabihf \
    cross-config \
    dpkg-cross
    
RUN apt install -y libstdc++-8-dev:armhf \
    crossbuild-essential-armhf \
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/*

COPY ./src/main.cpp ./   

RUN clang++  -target arm-linux-gnueabihf  main.cpp

RUN readelf -h a.out

RUN rm main.cpp && rm a.out




