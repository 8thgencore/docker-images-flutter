FROM ghcr.io/cirruslabs/android-sdk:34

LABEL org.opencontainers.image.source=https://github.com/8thgencore/docker-images-flutter

# Setup new user
RUN useradd -u 1000 -m -s /bin/bash user

# Give permission
USER root
RUN chown -R 1000:1000 /opt/android-sdk-linux
USER 1000

ENV HOME=/tmp

ENV ANDROID_HOME=/opt/android-sdk-linux \
    LANG=en_US.UTF-8 \
    LC_ALL=en_US.UTF-8 \
    LANGUAGE=en_US:en

ENV ANDROID_SDK_ROOT=$ANDROID_HOME \
    PATH=${PATH}:${ANDROID_HOME}/cmdline-tools/latest/bin:${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/emulator

ARG flutter_version

ENV FLUTTER_HOME=${HOME}/sdks/flutter \
    FLUTTER_VERSION=$flutter_version
ENV FLUTTER_ROOT=$FLUTTER_HOME

ENV PATH ${PATH}:${FLUTTER_HOME}/bin:${FLUTTER_HOME}/bin/cache/dart-sdk/bin

RUN git clone --depth 1 --branch ${FLUTTER_VERSION} https://github.com/flutter/flutter.git ${FLUTTER_HOME}

USER root
RUN yes | flutter doctor --android-licenses \
    && flutter config --android-sdk /opt/android-sdk-linux \
    && flutter doctor \
    && chown -R 1000:1000 ${FLUTTER_HOME}
USER 1000
